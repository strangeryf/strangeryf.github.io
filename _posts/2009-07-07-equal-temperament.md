---
layout: post
title:  "Equal temperament"
date:   2009-07-07
tags: Matlab music
---
Zhu Zaiyu discovered the twelve-tone equal temperament in 1584, and published this theory in his book Lulu Jingyi (律呂精義) 12 years later. The main idea is to devide an octave into 13 notes, where ratio of frequency between two immdiately adjacent notes is the 12th root of 2.

The Matlab code goes here
```matlab
alpha = 2^(1/12);   % 12-TET by Zhu Zaiyu (朱載堉), 1584 AD
c = 260.63;         % Unison (C), 260.63 Hz
x = 0:1/c/16:1;     % max of fs is 4*c, so we need 8~10 points per period, that makes 16*c
for i = 0:24        % Two octaves, each contains 12 notes
    j = mod(i, 12);
    if (j~=1 && j~=3 && j~=6 && j~=8 && j~=10)    % C D E F G A B [C]
        fs = c * alpha^i
        y = sin(2*pi*fs*x);
        subplot(2,1,1)
        plot(x,y)
        subplot(2,1,2)
        plot(x, abs(fft(y)))
        wavplay(y, 16*c);
    end
    pause(0.1)
end
for i = 24:-1:0
    j = mod(i, 12);   
    if (j~=1 && j~=3 && j~=6 && j~=8 && j~=10)     % [C] B A G F E D C
        fs = c * alpha^i
        y = sin(2*pi*fs*x);
        subplot(2,1,1)
        plot(x,y)
        subplot(2,1,2)
        plot(x, abs(fft(y)))
        wavplay(y, 16*c);
    end
    pause(0.1)
end
```
<embed src='http://player.youku.com/player.php/sid/XMTAzODIzNDE2/v.swf' allowFullScreen='true' quality='high' width='480' height='400' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash'/>