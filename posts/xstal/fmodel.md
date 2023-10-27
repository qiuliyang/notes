---
layout: post
title: "From Molecular Model to Sturctural Factor"
date: 2021-05-21
progress: 100%
permalink: /xtal/fcalc/
comments: true
---

{% epigraph 'Go back to definition!' 'George Polya' 'How to solve it' %}

In general, the following equation calculate the complex x-ray scattering factors from molecular models{% sidenote '1' 'Usually a PDB file, with infos of space group, atom type, atom position, iso/aniso B-factor, and occupancy in an asymmetric unit.' %}{% sidenote "2" "Rupp's textbook, P279" %}:

$$
F_{p} (\vec{h}) = \sum_G \sum_j O_j \cdot f_{\vec{h},j}\cdot\text{DWF}(\vec{h})\cdot\exp{[2\pi i \vec{h}\cdot(\mathbf{R}_G\vec{x}_j+\vec{T}_G)]} \tag{1}
$$

where: 

1. subscript $$p$$ of $$F_p$$ stands for "protein", as there is extra correction from solvent; 

2. $$\vec{h}$$ is the reciprocal index $$[h,k,l]$$; 

3. $$G$$ is the index of symmetry operations (appears as rotation matrix $$\mathbf{R}_G$$ and translation vector $$\vec{T}_G$$) belonging to the space group; 

4. $$j$$ is the index of atom; $$O_j$$ is the occupancy value the atom $$j$$; 

5. $$f_{\vec{h},j}$$ is the atomic scattering factor of atom $$j$$ at reciprocal space site $$[h,k,l]$$;

6. DWF is the debye-waller factor or B-factor, either isotropic or anisotropic

7. $$\vec{x}_j$$ is the <i class='contrast'>fractional</i> coordinates{% sidenote '3' 'In contrast to cartesian coordinates.' %} of atom $$j$$ in the unit cell.

I will cover discussions on practical calculation of some nontrivial terms mentioned above.

* listnotshown
{: toc}

### <i class='contrast'>Space group and symmetry operations</i>

As the atoms contained in the PDB file is an asymmetry unit, we have to apply all necessary symmetry operations on the asyymetry unit to complete the unit cell. The symmetry operations list is fully determined by the space group info, which is usually recorded as `CRYST1` entry in PDB file. For example in [`6QJI`](https://www.rcsb.org/structure/6QJI):

```
CRYST1   61.970   61.970  228.365  90.00  90.00 120.00 P 31 1 2
```
where the space group is $$P3_112$$, with operations{% sidenote '4' 'See Rupp Textbook P226 about how to translate Hermann-Mauguin symbol into list of operations.' %}: 
1. x, y, z

2. -y, x-y, z+1/3

3. -x+y, -x, z+2/3

4. -y, -x, -z+2/3

5. -x+y, y, -z+1/3

6. x, x-y, -z

Each operation can be represented as a rotation matrix $$\mathbf{R}_G$$ and a transliation vector $$\vec{T}_G$$, like for the opearation 2, (-y, x-y, z+1/3): 

$$
\mathbf{R}_G=\left[\begin{array}{rrr}
0 & -1 & 0\\
1 & -1 & 0 \\
0 & 0 & 1
\end{array}\right] \quad \vec{T}_G = [0,0,1/3]
$$

`gemmi` provides a good API to generate a complete list of operations based on the space group symbol:

```python
>>> symmetry = gemmi.SpaceGroup("P 31 1 2")
>>> operations = list[symmetry.operations()]
>>> print(operations[1], operations[1].rot, operations[1].tran)
<gemmi.Op("-y,x-y,z+1/3")> [[0, -24, 0], [24, -24, 0], [0, 0, 24]] [0, 0, 8]
```

### <i class='contrast'>Atomic Structure Factor</i>
Each atom will contribute to the overall structural factor based on its atom type, which is abstracted into an atomic scattering factor $$f_{\vec{h},j}$$. Here we approximate{% sidenote '5' 'drop the anomalous scattering' %} the actual atomic structural factor with a wavelength-independent one $$f_{\vec{h},j} \approx f^0_{\vec{h},j}$$ and present with an empirical function:

$$
f_{\vec{h},j}^0 = \sum_{i=1}^4a_i\cdot\exp[-b_i \cdot (\sin \theta/\lambda)^2] + c \tag{2}
$$

The nine parameters $$a_i, b_i,c$$ are the Cromer-Mann coefficients{% sidenote '6' 'can be found at International Tables for crystallography, Volume C' %} for each atom type.  And 

$$\sin\theta/\lambda = d^*_{hkl}/2 \tag{3}$$

where:

$$
\begin{aligned}
d_{h k l}^{*}&=\frac{1}{d_{h k l}}\\ &=\left(h^{2} a^{* 2}+k^{2} b^{* 2}+l^{2} c^{2}+2 h k a^{*} b^{*} \cos \gamma^{*}+2 h l a^{*} c^{*} \cos \beta^{*}+2 k l b c^{*} \cos \alpha^{*}\right)^{1 / 2}
\end{aligned}$$

The annotations with superscript $$*$$ are geometry parameters of the reciprocal cell{% sidenote '7' "see Rupp's textbook P747-748 for a complete transformation equations" %}. 

Practically, we can create a search list based on the ITC tables from scratch and take each $$d^*_{hkl}$$ in, or we can also use the good API `gemmi` provides for a neat calculation: 

```python
atom_O = gemmi.Element('O')
atom_O.it92.calculate_sf(dr_sq/4)
```

### <i class='contrast'>Isotropic and Anisotropic Debye-Waller Factor</i>
Atoms in crystal lattice or in a molecule are not fixed to a absolutely rigid positions, but they will vibrate around a mean position. The atoms can also be displaced because of disorder. As a restult, in each unit cell the atoms tend to be at a slightly different position. To account for the additional phase difference from this effect, an extra gaussian, wavelength-dependent term is introduced, called Debye-Waller factor, usually parameterized with B-factor in crystallography field. 

Generally, $$\text{DWF}(\vec{h})= \exp[-2\pi\langle((\mathbf{O}^{-1})^T\vec{h}\cdot \vec{u})\rangle]$${% sidenote '8' "$$\mathbf{O}^{-1}$$ is the deorthogoniazation matrix of the unit cell, see Rupp's textbook P746." %}, where $$\vec{u}$$ is the displacement vector of the atom. 

In isotropic case, the displacement vector $$\vec{u}$$ is replaced with the isotropic amplitude $$u$$ related to B-factor via:

$$
B=8\pi^2\langle u^2\rangle
$$

So the DWF becomes a standard Gaussian B-factor exponential:

$$
\text{DWF}_{iso}(\vec{h}) = \exp[-B_{iso}(\sin\theta/\lambda)^2] \tag{4}
$$

The isotropic B-factors are recorded in each `ATOM` entry of the PDB file, for example the `51.55` in the following line copied from `3I4W`:

```
ATOM      1  N   GLU A 305       2.491 -15.524  -5.091  1.00 51.55           N  
```

In anisotropic case, the displacement is usually parameterized with a symmetric matrix $$U$$, transforming the DWF into:

$$\begin{aligned}
\text{DWF}_{aniso}(\vec{h})=\exp[-2\pi^2(&U^{11}h^2a^{*2}+ U^{22}k^2b^{*2} + U^{33}l^2c^{*2} 
\\+ & 2U^{12}hka^*b^*\cos\gamma^*  
\\+ & 2U^{13}hla^*c^*\cos\beta^* 
\\+ & 2U^{23}klb^*c^*\cos\alpha^* )]
\end{aligned} \tag{5}$$

For atoms with anisotropic displacement info, the 6 elements of matrix $$U$$ are recorded in the `ANISOU` entry following the `ATOM` entry in PDB file (multiplied by $$10^4$$), for example:

```
ATOM      1  N   ASP A 306       5.898  73.370  26.068  1.00 60.22           N
ANISOU    1  N   ASP A 306     9135   7719   6029   1853  -1562   -620       N
```

The `60.22` value in the isotropic B-factor place is the isotropic B-factor equivalent $$B_{eq} = \frac{8\pi^2}{3}(U^{11}+U^{22}+U^{33})$$. 