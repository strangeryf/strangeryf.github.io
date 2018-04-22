---
layout: post
title:  "Some Matlab tips"
date:   2005-05-15
tags: Matlab
---
0. The contour funtion with parameters contour(Z,n) behaves strange: the whole plane is divided into n+1 sections by n isovalue lines, and the difference between adjacent lines is (max(Z)-min(Z))/(n+1). The number of contour levels and the values of the contour levels are chosen automatically based on the minimum and maximum values of Z.

1. The contour of wavelet coefficients matrix of a sound signal varies from wavelets to wavelets. The Daubechies wavelets, Symlets, Coiflets, Biorthogonal wavelets, Reverse biorthogonal wavelets, Meyer wavelet, Discrete approximation of Meyer wavelet, Gaussian wavelets, Mexican hat wavelet and Morlet wavelet give seperated spectra, while Complex Gaussian wavelets, Shannon wavelets, Frequency B-Spline wavelets and Complex Morlet wavelets give concentrated spectra. Maybe the abs operation in my program contributes to this effect.

2. Some complex wavelets display lots of horrible small pots in the time-scale sp, while others do not. The suspicious complex wavelets include: shan1-1.5  shan1-1 shan1-0.5 shan1-0.1 shan2-3(somewhat better), all Frequency B-Spline wavelets except fbsp2-1-1(somewhat better),  cmor1-0.5 cmor1-0.1. Some good complex waveltes are Complex Gaussian wavelets, cmor1-1.5, cmor1-1.

3. Graphic representation of discrete analysis: time is on the abscissa and on the ordinate the scale a is dyadic Graphic representation of continuous analysis: time is on the abscissa and on the ordinate the scale varies almost continuously. Keep in mind that when a scale is small, only small details are analyzed, as in a geographical map.

4. Matlab use "~=" not "!=", "~" not "!" as logic operator.

5. Matlab operator (:) after a vector can convert that vector to a column vector.

6. fix: Round towards zero, floor: Round towards minus infinity, ceil: Round toward infinity

7. If you know the exact position of the part of matrix of vector you want, you can use the follwoing code to extract them:
k = x(first:last);

8. In Matlab, the operator : has a lower priority than +, -, *, / etc.
