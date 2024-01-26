#+title: Windows

* Remove Windows Bloatware
iwr -useb https://git.io/debloat|iex

* WSL Config (.wslconfig)
[experimental]
autoMemoryReclaim=gradual
networkingMode=mirrored
dnsTunneling=true
firewall=true
autoProxy=true
