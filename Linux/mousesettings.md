### Save this

```
#~/.xinitrc
xinput set-prop 8 267 1.5
xinput set-prop 8 268 5
xinput set-prop 8 269 10 
```

```
default was:
Constant Deceleration (273): 1.0
Adaptive Deceleration (274): 1.0
Velocity Scaling (275): 10.0

xinput
xinput list-props 10
xinput set-prop 10 273 2

273: 2 (speed)
274: 20 (slow down) 
275: 20 (multiplier)

xorg.conf:
#Section "InputClass"
#  Identifier "My Mouse"
#	MatchIsPointer "yes"
	# set the following to 1 1 0 respectively to disable acceleration.
#	Option "AccelerationNumerator" "2"
#	Option "AccelerationDenominator" "1"
#	Option "AccelerationThreshold" "4"
#EndSection

#This works on beast:
Section "InputClass"
	Identifier "My Mouse"
	MatchIsPointer "yes"
# some curved deceleration
	Option "AdaptiveDeceleration" "2"
# linear deceleration (mouse speed reduction)
	Option "ConstantDeceleration" "2"
EndSection
```
