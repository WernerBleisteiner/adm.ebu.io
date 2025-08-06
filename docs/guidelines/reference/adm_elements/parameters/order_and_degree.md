# order and degree

The `order` and `degree` parameters appear in [`audioBlockFormat`](../audio_channel_format_hoa.md#audioblockformat) only for the 'HOA' typeDefinition.


The meaning of order and degree values is based on the following definition of real-valued spherical harmonics:

$$
Y_n^m(\theta,\phi) = N_n^{|m|}P_n^{|m|}\cos(\theta)
\begin{cases}
  \sqrt{2}\cos(m\phi), & \text{for}\ m > 0\\
  1, & \text{for}\ m = 0\\
  -\sqrt{2}\sin(m\phi), & \text{for}\ m < 0
\end{cases}
$$

Where:

 - \(n\) is the order value, \(m\) is the degree value, \(\phi\) is azimuth, and \(\theta\) is elevation
 - \(N_n^{|m|}\) is the normalization parameter for the given order and degree
 - \(P_n^{|m|}\) is the associated Legendre function for the given order and degree.

The associated Legendre functions \(P_n^m(x)\) are defined as:

$$P_n^m(x) = \left(1-x^2\right)^{\frac{m}{2}}  \frac{d^m}{dx^m}  P_n(x),\quad m≥0$$

with the Legendre polynomial \(P_n(x)\) and without the Condon-Shortley phase term \((-1)^m\).
