---
title: MakeGridDHC()
keywords: spherical harmonics software package, spherical harmonic transform, legendre functions, multitaper spectral analysis, Python, gravity, magnetic field
sidebar: mydoc_sidebar
permalink: pymakegriddhc.html
summary:
tags: [python]
toc: false
editdoc: pydoc
---

Create a 2D complex map from a set of complex spherical harmonic coefficients that conforms with Driscoll and Healy's (1994) sampling theorem.

## Usage

griddh = MakeGridDHC (cilm, [lmax, norm, sampling, csphase, lmax_calc, extend])

## Returns

griddh : complex, dimension (nlat, nlong)
:   A 2D complex map of the input spherical harmonic coefficients cilm that conforms to the sampling theorem of Driscoll and Healy (1994). If sampling is 1, the grid is equally sampled and is dimensioned as (n by n), where n is 2lmax+2. If sampling is 2, the grid is equally spaced and is dimensioned as (n by 2n). The first latitudinal band of the grid corresponds to 90 N, the latitudinal sampling interval is 180/n degrees, and the default behavior is to exclude the latitudinal band for 90 S. The first longitudinal band of the grid is 0 E, by default the longitudinal band for 360 E is not included, and the longitudinal sampling interval is 360/n for an equally sampled and 180/n for an equally spaced grid, respectively. If extend is 1, the longitudinal band for 360 E and the latitudinal band for 90 S will be included, which increases each of the dimensions of the grid by 1.

## Parameters

cilm : complex, dimension (2, lmaxin+1, lmaxin+1)
:   The complex spherical harmonic coefficients of the function.  The first index specifies the coefficient corresponding to the positive and negative order of m, respectively, with Clm=cilm[0,l,m] and Cl,-m=cilm[1,l,m)].

lmax : optional, integer, default = lmaxin
:   The maximum spherical harmonic degree of the function, which determines the sampling n of the output grid.

norm : optional, integer, default = 1
:   1 = 4-pi (geodesy) normalized harmonics; 2 = Schmidt semi-normalized harmonics; 3 = unnormalized harmonics;  4 = orthonormal harmonics.

sampling : optional, integer, default = 1
:   If 1 (default) the input grid is equally sampled (n by n). If 2, the grid is equally spaced (n by 2n).

csphase : optional, integer, default = 1
:   1 (default) = do not apply the Condon-Shortley phase factor to the associated Legendre functions; -1 = append the Condon-Shortley phase factor of (-1)^m to the associated Legendre functions.

lmax_calc : optional, integer, default = lmax
:   The maximum spherical harmonic degree used in evaluating the  function. This must be less than or equal to lmax, and does not affect the number of samples of the output grid.

extend : input, optional, bool, default = False
:   If True, compute the longitudinal band for 360 E and the latitudinal band for 90 S. This increases each of the dimensions of griddh by 1.

## Description

MakeGridDHC will create a 2-dimensional complex map equally sampled (n by n) or equally spaced (n by 2n) in latitude and longitude from a set of input complex spherical harmonic coefficients, where N is 2lmax+2. This grid conforms with the sampling theorem of Driscoll and Healy (1994) and this routine is the inverse of SHExpandDHC. The function is evaluated at each longitudinal band by inverse Fourier transforming the exponential terms for each degree l, and then summing over all degrees. When evaluating the function, the maximum spherical harmonic degree that is considered is the minimum of lmax, the size of cilm-1, or lmax_calc (if specified).

The default is to use an input grid that is equally sampled (n by n), but this can be changed to use an equally spaced grid (n by 2n) by the optional argument sampling. The redundant longitudinal band for 360 E and the latitudinal band for 90 S are excluded by default, but these can be computed by specifying the optional argument extend. The employed spherical harmonic normalization and Condon-Shortley phase convention can be set by the optional arguments norm and csphase; if not set, the default is to use geodesy 4-pi normalized harmonics that exclude the Condon-Shortley phase of (-1)^m.

The normalized legendre functions are calculated using the scaling algorithm of Holmes and Featherstone (2002), which are accurate to about degree 2800. The unnormalized functions are accurate only to about degree 15.

## References

Driscoll, J.R. and D.M. Healy, Computing Fourier transforms and convolutions on the 2-sphere, Adv. Appl. Math., 15, 202-250, 1994.

Holmes, S. A., and W. E. Featherstone, A unified approach to the Clenshaw summation and the recursive computation of very high degree and order normalised associated Legendre functions, J. Geodesy, 76, 279-299, 2002.
