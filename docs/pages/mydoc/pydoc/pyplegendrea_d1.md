---
title: PLegendreA_d1()
keywords: spherical harmonics software package, spherical harmonic transform, legendre functions, multitaper spectral analysis, Python, gravity, magnetic field
sidebar: mydoc_sidebar
permalink: pyplegendrea_d1.html
summary:
tags: [python]
toc: false
editdoc: pydoc
---

Compute all the unnormalized associated Legendre functions and first derivatives.

## Usage

p, dp = PLegendreA_d1 (lmax, z, [csphase])

## Returns

p : float, dimension ((lmax+1)\*(lmax+2)/2)
:   An array of unnormalized associated Legendre functions up to degree lmax. The index corresponds to l*(l+1)/2+m.

dp : float, dimension ((lmax+1)\*(lmax+2)/2)
:   An array of the first derivatives of the unnormalized associated Legendre functions up to degree lmax. The index corresponds to l*(l+1)/2+m.

## Parameters

lmax : integer
:   The maximum degree of the associated Legendre functions to be computed.

z : float
:   The argument of the associated Legendre functions.

csphase : optional, integer, default = 1
:   If 1 (default), the Condon-Shortley phase will be excluded. If -1, the Condon-Shortley phase of (-1)^m will be appended to the associated Legendre functions.

## Description

PLegendreA_d1 will calculate all of the unnormalized associated Legendre functions and first derivatives up to degree lmax for a given argument. These are calculated using a standard three-term recursion formula and hence will overflow for moderate values of l and m. The index of the array corresponding to a given degree l and angular order m corresponds to l*(l+1)/2+m. The integral of the associated Legendre functions over the interval [-1, 1] is 2*(l+m)!/(l-m)!/(2l+1). The default is to exclude the Condon-Shortley phase, but this can be modified by setting the optional argument csphase to -1. Note that the derivative of the Legendre polynomials is calculated with respect to its arguement z, and not latitude or colatitude. If z=cos(theta), where theta is the colatitude, then it is only necessary to multiply dp by -sin(theta) to obtain the derivative with respect to theta.
