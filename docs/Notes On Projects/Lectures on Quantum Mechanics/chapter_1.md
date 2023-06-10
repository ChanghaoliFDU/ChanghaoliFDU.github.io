# Chapter 1: Particle States in a Central Potential

##  Schrödinger Equation for a Central Potential

Any of one component of angular momentum $\mathbf{L}=\mathbf{x}\times\mathbf{p}\equiv-i\hbar\mathbf{x}\times\nabla$ commutes with the Hamiltonian $\mathbf{H}$. $\mathbf{L}^2$ also commutes with $\mathbf{H}$.

In polar coordinates,
$$
\begin{eqnarray}
\nonumber L_1&=&i\hbar\left(\sin\phi\frac{\partial}{\partial\theta}+\cot\theta\cos\phi\frac{\partial}{\partial\phi}\right)\\
\nonumber L_2&=&i\hbar\left(-\cos\phi\frac{\partial}{\partial\theta}+\cot\theta\sin\phi\frac{\partial}{\partial\phi}\right)\\
L_3&=&-i\hbar\frac{\partial}{\partial\phi}
\end{eqnarray}
$$
What does this have to do with the Schrödinger equation? 
$$
\mathbf{L}^2=-\hbar^2\left[r^2\nabla^2-\frac{\partial}{\partial r}r^2\frac{\partial}{\partial r} \right]
$$
or in other words: 
$$
\nabla^2=\frac{1}{r^2}\frac{\partial}{\partial r}r^2\frac{\partial}{\partial r}-\frac{\mathbf{L}^2}{\hbar^2r^2}
$$

Then Schrödinger equation takes the form:
$$
E\psi(\mathbf{x})=-\frac{\hbar^2}{2\mu r^2}\frac{\partial}{\partial r}\left(r^2\frac{\partial\psi(\mathbf{x})}{\partial r}\right)+\frac{1}{2\mu r^2}\mathbf{L}^2\psi(\mathbf{x})+V(r)\psi(\mathbf x)
$$
As long as $V(r)$ is not extremely singular at $r=0$, the wave function can be expressed as a power series in the Cartesian components.
$$
\psi(\mathbf x)\to r^lY(\theta,\phi)
$$
then,
$$
\mathbf{L}^2\psi(\mathbf x)=\hbar^2\frac{\partial}{\partial r}\left(r^2\frac{\partial\psi(\mathbf x)}{\partial r}\right)+2\mu r^2\left[E-V(r)\right]\psi(\mathbf x)
$$


In the limit $r\to 0$, as long as the potential is less singular than $1/r^2$, the second term on the right side vanishes as $r \to 0$ more rapidly than $\psi$, so $\psi$ satisfy the eigenvalue equation
$$
\mathbf{L}^2\psi(\mathbf x)\to\hbar^2l(l+1)\psi
$$
Hence, the eigenvalue of $\hat{H}$ can only be $\hbar^2l(l+1)$.

Since $\mathbf{L}^2$ acts only on angles,such 
$$
\psi(\mathbf x)=R(r)Y(\theta,\phi)
$$
where $R(r)$ is a function of $r$ satisfying
$$
R(r) \propto r^l\quad \text{for}\quad r\to 0
$$
and $Y(\theta,\phi)$ is a function of $\theta$ and $\phi$ satisfying
$$
\mathbf L^2Y=\hbar^2l(l+1)Y
$$
If we also require $\psi$ to be an eigenfunction of $L_3$ with eigenvalue denoted $\hbar m$ 

then 
$$
L_3Y=\hbar mY
$$
Equation 1.3 shows that $Y(\theta,\phi)$ must then have a $\phi$-dependence
$$
Y(\theta,\phi)=e^{im\phi}\times\text{function of}\quad\theta
$$
The condition that $Y(\theta,\phi)$ must have the same value at $\phi=0$ and $\phi=2\pi$ requires then $m$ be an integer.

##  Spherical Harmonics

 The angular part of the wave function will therefore be labeled with $l$ and $m$, as $Y_l^m(\theta,\phi)$. 

 Use Eq.3 and act on $r^lY_l^m$, and according to Eq.10, 
$$
\nabla^2\left(r^lY_l^m\right)=0
$$
Finally, recall that $r^lY_l^m(\theta,\phi)$ is a homogeneous polynomial of order $l$ in the Cartesian components of the coordinate vector $\mathbf x$. Equivalently, it can be written as a homogeneous polynomial of order $l$ in
$$
x_{\pm}\equiv x_1\pm ix_2=r\sin\theta e^{\pm i\phi}\quad\text{and}\quad x_3=r\cos\theta
$$
Thus Eq.11 tells us that $Y_l^m$ must contain numbers $\nu_{\pm}$ of factors of $x_{\pm}$ such that 
$$
m=\nu_+-\nu_-
$$
Since the total number of factors of $x_+$, $x_-$ and $x_3$ is $l$, the index $m$ is a positive or negative integer, with a maximum value $l$ and a minimum value $-l$. 

Whether $Y^m_l$ is uniquely determined by the values of $l$ and $m$ ?

For a given $l$ , $m$ takes $2l+1$ values. And we have
$$
N_l=\sum^{l}_{\nu_+=0}\sum^{l-\nu_+}_{\nu_-=0}1=\frac 12(l+1)(l+2)
$$
Recall Eq.13,
$$
N_l-N_{l-2}=2l+1
$$
Thus, there is only one independent polynomial for each $l$ and $m$. 

These functions, denoted $Y_l^m(\theta,\phi)$, with $-l\le m\le +l$, are known as **spherical harmonics**.
$$
Y_l^m(\theta,\phi)\propto P_l^{|m|}(\theta)e^{im\phi}
$$
For $l\le 2$,
$$
\begin{eqnarray}
\nonumber Y_0^0&=&\sqrt{\frac{1}{4\pi}}\\
\nonumber Y_1^1&=&-\sqrt{\frac{3}{8\pi}}(\hat{x}_1+i\hat{x}_2)=-\sqrt{\frac{3}{8\pi}}\sin\theta e^{i\phi}\\
\nonumber Y_1^0&=&-\sqrt{\frac{3}{4\pi}}\hat{x}_3=-\sqrt{\frac{3}{4\pi}}\cos\theta\\
\nonumber Y_1^{-1}&=&-\sqrt{\frac{3}{8\pi}}(\hat{x}_1-i\hat{x}_2)=-\sqrt{\frac{3}{8\pi}}\sin\theta e^{-i\phi}
\end{eqnarray}
$$

We also note the space-inversion(or "**parity**") property of the wave function.

Under the transformation $\hat{x}\to-\hat{x}$, the spherical harmonics change by just a sign factor $(-1)^l$:
$$
Y_l^m(\pi-\theta,\pi+\phi)=(-1)^lY_l^m(\theta,\phi)
$$


## The Hydrogen Atom

Since we have Eq.8, $\psi(\mathbf x)=R(r)Y(\theta,\phi)$, and associate it with Eq.10, $\mathbf L^2Y=\hbar^2l(l+1)Y$

we can get Schrödinger equation；
$$
E\ R(r)=-\frac{\hbar^2}{2\mu r^2}\frac{\mathrm d}{\mathrm dr}\left(r^2\frac{\mathrm dR(r)}{\mathrm dr}\right)+\frac{\hbar^2l(l+1)}{2\mu r^2}R(r)+V(r)R(r)
$$
The equation above can be made to look more like the Schrödinger equation in one dimension by defining a new radial wave function
$$
u(r)\equiv rR(r)
$$
Then Eq.20 takes the form
$$
-\frac{\hbar^2}{2\mu}\frac{\mathrm d^2u(r)}{\mathrm dr^2}+\left[V(r)+\frac{l(l+1)\hbar^2}{2\mu r^2}\right]r(r)=E\ u(r)
$$
Consider $V(r)=-Ze^2/r$
$$
-\frac{\mathrm d^2u(r)}{\mathrm dr^2}+\left[-\frac{2m_eZe^2}{r\hbar^2}+\frac{l(l+1)}{r^2}\right]u(r)=-\kappa^2u(r)
$$
where $\kappa$ is defined by
$$
E=-\frac{\hbar^2\kappa^2}{2m_e},\quad \kappa>0
$$
We can write this in dimensionless form by introducing
$$
\rho\equiv\kappa r
$$
After dividing by $\kappa^2$, Eq.23 becomes
$$
-\frac{\mathrm d^2u}{\mathrm d\rho^2}+\left[-\frac{\xi}{\rho}+\frac{l(l+1)}{\rho^2}\right]u=-u
$$
where
$$
\xi\equiv \frac{2m_eZe^2}{\kappa\hbar^2}
$$
We must look for a solution that decreases as $\rho^{l+1}$ for $\rho\to 0$, and like $\exp(-\rho)$ for $\rho\to\infin$, so let's replace $u$ with a new function $F(\rho)$, defined by 
$$
u=\rho^{l+1}\exp(-\rho)F(\rho)
$$
The radial wave equation (26) thus becomes
$$
\frac{\mathrm d^2F}{\mathrm d\rho^2}-2\left(1-\frac{l+1}{\rho}\right)\frac{\mathrm dF}{\mathrm d\rho}+\left(\frac{\xi-2l-2}{\rho}\right)F=0
$$
Let's try a power-series solution
$$
F=\sum^{\infin}_{s=0}a_s\rho^s,
$$
Then Eq.29 becomes,
$$
\sum^{\infin}_{s=0}a_s\left[s(s-1)\rho^{s-2}-2s\rho^{s-1}+2s(l+1)\rho^{s-2}+(\xi-2l-2)\rho^{s-1}\right]=0
$$
After redefining $s$ as $s+1$, 
$$
\sum^{\infin}_{s=0}\rho^{s-1}\left[s(s+1)a_{s+1}-2sa_s+2(s+1)(l+1)a_{s+1}+(\xi-2l-2)a_s\right]=0
$$
Thus
$$
(s+2l+2)(s+1)a_{s+1}=(-\xi+2s+2l+2)a_s
$$
Let us consider the asymptotic behavior of this power series for large $\rho$.

For $s\to\infin$:
$$
a_{s+1}/a_s\to 2/s
$$
we have
$$
a_s\approx C\;2^s/(s+B)!
$$
Thus we expect that asymptotically
$$
F(\rho)\approx C\sum^{\infin}_{s=0}\frac{(2\rho)^s}{(s+B)!}\to C(2\rho)^{-B}e^{2\rho}
$$
Aside from constants and powers of $\rho$, $u\approx \exp(\rho)$, which is ***inconsistent*** with Eq.28. 

***The only way to avoid this is to require that the power series terminates.***
$$
\xi=2n\ge l+1 \quad \text{see right hand of Eq. 33}
$$
Although the wave functions depend on $l$ and $m$, the energy only depend on $n$. with $\xi=2n$, Eq.27 gives 
$$
\kappa_n=\frac{2m_eZe^2}{\xi\hbar^2}=\frac{1}{na}
$$
where $a$ is *Bohr radius*
$$
a=\frac{\hbar^2}{m_eZe^2}=5.2918\times10^{-10}Z^{-1}\mathrm m
$$
Finally,
$$
E_n=-\frac{\hbar^2\kappa_n^2}{2m_e}=-\frac{\hbar^2}{2m_ea^2n^2}=-\frac{m_eZ^2e^4}{2\hbar^2n^2}=-\frac{13.6057Z^2\mathrm{eV}}{n^2}
$$
For each $n$ we have $l$ values running from $0$ to $n-1$, and for each $l$ we have $2l+1$ values of $m$. The total number of states with energy $E_n$ is 
$$
\sum^{n-1}_{l=0}(2l+1)=n^2
$$
The rate at which a state represented by a wave function $\psi$ decays by single-photon emission into a state represented by a wave function $\psi'$ is proportion to $|\int\psi'^*\mathbf x\psi|^2$. If we change the variable of integration from $\mathbf x$ to $-\mathbf x$, the wave functions $\psi$ and $\psi'$ change by factors $(-1)^l$ and $(-1)^{l'}$, and so the whole integrand changes by a factor 
$$
(-1)^{l+l'+1}
$$
So the signs $(-1)^l$ and $(-1)^{l'}$ must be opposite. Thus $2p$ orbital can transit to $1s$, but $2s$ can't transit to $1s$ by only emitting one photon.

## The two body problem

The two-body problem is equivalent to a one body problem, with the electron  mass replaced with a reduced mass:
$$
\mu=\frac{m_em_N}{m_e+m_N}
$$
The Hamiltonian for one-electron atom is
$$
H=\frac{\mathbf P_e^2}{2m_e}+\frac{\mathbf P_N^2}{2m_N}+V(\mathbf x_e-\mathbf x_N)
$$
We introduce a relative coordinate $\mathbf x$ and a center-of-mass coordinate $\mathbf X$ by
$$
\mathbf x\equiv\mathbf x_e-\mathbf x_N,\quad \mathbf X\equiv\frac{m_e\mathbf x_e+m_N\mathbf x_N}{m_e+m_N}
$$
and a relative momentum $\mathbf p$ and a total momentum $\mathbf P$ by
$$
\mathbf p\equiv\mu\left(\frac{\mathbf p_e}{m_e}-\frac{\mathbf p_N}{m_N}\right),\quad \mathbf P\equiv \mathbf p_e+\mathbf p_N
$$
 Then Hamiltonian may be written 
$$
H=\frac{\mathbf p^2}{2\mu}+\frac{\mathbf P^2}{2(m_e+m_N)}+V(\mathbf x)
$$
where
$$
\mathbf p=-i\hbar\nabla_{\mathbf x},\quad \mathbf P=-i\hbar\nabla_{\mathbf X}
$$
So the momenta and the coordinates satisfy the commutation relations
$$
[x_i,p_j]=[X_i,P_j]=i\hbar\delta_{ij},\quad[x_i,P_j]=[X_i,p_j]=0
$$
Such a wave function will have the form
$$
\psi(\mathbf x,\mathbf X)=e^{i\mathbf P\cdot\mathbf X/\hbar}\psi(\mathbf x)
$$
and $\psi(\mathbf x)$ is a wave function for an internal energy $\mathcal{E}$, satisfying the one-particle Schrödinger equation
$$
-\frac{\hbar^2\nabla_x^2\psi(\mathbf x)}{2\mu}+V(\mathbf x)\psi(\mathbf x)=\mathcal{E}\psi(\mathbf x)
$$
The total energy is just the internal energy $\mathcal{E}$ of the atom, plus the kinetic energy of its overall motion:
$$
E=\mathcal{E}+\frac{\mathbf P^2}{2(m_e+m_N)}
$$
For hydrogen and deuteron,
$$
\mu_{pe}=0.99945m_e,\quad\mu_{de}=0.99973m_e.
$$
This tiny difference is enough to produce a detectable split in the frequencies of light emitted from a mixture of ordinary hydrogen and deuterium.

## The Harmonic Oscillator

Let's consider a particle of mass $M$ in a potential 
$$
V(r)=\frac 12M\omega^2r^2
$$
There are four reason it is worth considering

1. Historical Reason: This is the problem studied by Heisenberg introducing *Matrix Mechanics* 
2. This theory provides a nice illustration of how we can find energy levels and radiative transition amplitudes by algebraic methods, ***without having to solve second-order differential equations***.
3. The harmonic potential is used in models of atomic nuclei.
4. The methods described here is useful for dealing with **the energy levels of electrons in magnetic fields** and for calculating **the properties of photons**.

The Schrödinger equation is here
$$
E\;\psi=-\frac{\hbar^2}{2M}\nabla^2\psi+\frac 12M\omega^2r^2\psi
$$
we can write this equation in another form
$$
\sum^{3}_{i=1}\left(-\frac{\hbar^2}{2M}\frac{\partial^2\psi}{\partial x_i^2}+\frac{M\omega^2x_i^2\psi}{2}\right)=E\ \psi
$$
This has separable solutions, of the form
$$
\psi(\mathbf x)=\psi_{n_1}(x_1)\psi_{n_2}(x_2)\psi_{n_3}(x_3)
$$
where $\psi_n(x)$ is a solution of the one-dimensional Schrödinger equation
$$
-\frac{\hbar^2}{2M}\frac{\partial^2\psi_n(x)}{\partial x^2}+\frac{M\omega^2x^2\psi_n(x)}{2}=E_n\psi_n(x)
$$
The energy is the sum.
$$
E=E_1+E_2+E_3
$$
To solve this problem, we introduce so-called lowering and raising operators
$$
\begin{eqnarray}
a_i\equiv\frac{1}{\sqrt{2M\hbar\omega}}\left(-i\hbar\frac{\partial}{\partial x_i}-iM\omega x_i\right)\\
a^{\dagger}_i\equiv\frac{1}{\sqrt{2M\hbar\omega}}\left(-i\hbar\frac{\partial}{\partial x_i}+iM\omega x_i\right)
\end{eqnarray}
$$
These operators obey the commutation relations
$$
\left[a_i,a_j^{\dagger}\right]=\delta_{ij}
$$
and 
$$
\left[a_i,a_j\right]=\left[a_i^{\dagger},a_j^{\dagger}\right]=0
$$
Also, the one-dimensional Hamiltonian here is 
$$
H_i\equiv-\frac{\hbar^2}{2M}\nabla^2_i+\frac{M\omega^2x_i^2}{2}=\hbar\omega\left[a_i^{\dagger}a_i+\frac12\right]
$$
Now
$$
[H_i, a_i]=-\hbar\omega a_i,\quad [H_i,a_i^{\dagger}]=+\hbar\omega a_i^{\dagger}
$$
Hence if $\psi$ represents a state with energy $E$, then $a_i\psi$ represents a state with energy $E-\hbar \omega$, and $a_i^{\dagger}\psi$ represents a state with energy $E+\hbar\omega$.

There must be a wave function $\psi_0(x_i)$ for which $a_i\psi_0=0$; it is
$$
\psi_0(x_i)\propto\exp(-M\omega x_i^2/2\hbar)
$$

And 
$$
\psi_{n_i}(x_i)\propto a_i^{\dagger n_i}\psi_0(x_i)\propto H_{n_i}(x_i)\exp(-M\omega x_i^2/2\hbar)
$$
where $H_n(x)$ is a polynomial of order $n$ in x. These polynomials satisfy the parity condition
$$
H_n(-x)=(-1)^nH_n(x)
$$
The general wave function representing a state of definite energy is therefore
$$
\psi_{n_1n_2n_3}(\mathbf x)\propto a_1^{\dagger n_1}a_2^{\dagger n_2}a_3^{\dagger n_3}\propto H_{n_1}(x_1)H_{n_2}(x_2)H_{n_3}(x_3)\exp(-M\omega r^2/2\hbar)
$$
and the state has energy
$$
E_{n_1n_2n_3}=\hbar\omega\left[\sum_i\left(a_i^{\dagger}a_i+\frac 12\right)\right]=\hbar\omega\left[N+\frac 32\right]
$$
where $N=n_1+n_2+n_3$.

The degeneracy $\mathcal{N}_n$
$$
\mathcal{N}_n=\sum^N_{n_1=0}\sum^{N-n_1}_{n_2=0}1=\sum^{N}_{n_1=0}(N-n_1+1)=\frac{(N+1)(N+2)}{2}
$$
