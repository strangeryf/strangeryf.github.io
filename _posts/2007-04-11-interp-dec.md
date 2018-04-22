---
layout: post
title:  "Interpolation and Decimation"
date:   2007-04-11
tags: DSP
---
If somebody does interpolation by fitting a line or parabola between two samples he or she has not read enough dsp books. These methods will end up in aliasing and/or distortion.

original post: http://www.harmony-central.com/Effects/audio-effects-faq-10.txt

[by Tom Ahola]

    If the sample rate is to be drop to 1/2 you first have to
    filter out the top half of the bandwidth (spectrum over Sr/4 !)
    and after that you can throw away every second sample. (resampling)
    If the lowpass filter is ideal (brick wall) no extra noise is
    added, you only loose half the bandwidth.

    In interpolation to double sample rate you first add a zero
    between each sample (resampling). This gives no additional
    white noise or any distortion, you just end up with a spectrum
    that is doubled (imaged). To remove the undesired spectral image
    you have to lowpass filter the resampled signal with a
    filter with a bandwidth of Sr/4, where Sr is now the new sample
    rate. If the filter is ideal, the signal is identical to the original
    signal (no noise!).

    You can interpolate/decimate by any integer, rational or decimal
    number. Rational interp./decim. can be done efficiently by the
    use of polyphase filters.

    If somebody does interpolation by fitting a line or parabola
    between two samples he or she has not read enough dsp books.
    Theese methods will end up in aliasing and/or distortion.

    +    Tom Ahola       Metrology Research Institute, Finland
    +      E-mail: tom.ahola@hut.fi      WWW: http://www.hut.fi/~tahola/

The Method of doing sample rate conversion tought in my DSP course was to
perform a fourier transform (ie FFT or DFT) on the signal and then do a reverse
transform, with extra zero padded values (increasing rate) or with less high
frequency components (decreasing rates).  Ie the reverse transform is done on
more or less frequency components than the original. I dont know whether this
system is better than Toms method, or if the extra complexity has no actual
benefit. My gut feeling is that this is better, especially for non integer rate
changes, but for down conversion I can see that some windowing may be needed.
