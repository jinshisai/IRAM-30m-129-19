Project summary
---------------
README file for the project 129-29
PI name and e-mail: Jinshi Sai
                    jsai@asiaa.sinica.edu.tw

This project aims at mapping the C18O (2-1) and N2H+ (1-0) line
emission in the three Class I protostars, TMC-1A, TMC1 and TMR1 with the IRAM-30m.

We propose to integrate until reaching a rms of 70mK, 100 mK, and 50 mK on TMC-1A, TMC1, and TMR1, respectively, to detect the line emission of C18O, N2H+, HCO+, and 13CO.


Observation setup
-----------------
We use the EMIR receivers together with the FTS backend at 50 kHz
resolution. The two lines are observed simulateously, in dual band
mode (E090 and E230). The FTS backend at a 50 kHz is used in parallel
with VESPA.

We use the OTF PSW observing mode to cover a region of ~ 2' x 2'. The requested sensitivities per 0.14 km s-1 channel for TMC-1A, TMC1, and TMR1 are 70mK, 100 mK, and 50 mK, respectively. These sensitivities should be reached in ~8hr, ~5hr and ~12hr of telescope time, respectively, assuming average winter conditions (4.0 mm of PWV).

Three targets will be observed one by one. Once a source is completed, we will go to the next target.


Typical PAKO session
--------------------

```
! Startup
!--------

>gopako
>pakodisplay
>pako

PAKO> pako\set dosubmit yes
PAKO> pako\set level 3 3

@ ini
set point 0 0
set focus -2

! Select a planet, set the receivers and backend and do a calibration
! to send the receiver setup. This also moves the telescope to the
! planet.

source mars
@ receiver-c18o
@ backend-c18o
calibrate /default
start
pause "Ready to tune the receivers."

! Do another calibration to check if the system temperatures are OK

calibrate /default
start
pause "Please check that the system temperatures are OK."

! Do a pointing and a focusing on Mars

set focus -2       ! a good starting point
@ pointing-mars
pause "Please enter the pointing corrections."
set point  Az El

@ focus
pause "Please enter the focus corrections."
set focus FF

! Do a pointing on a strong quasar close to the target source.

!pointing with the nearby source, Mars
sou mars
@ pointing-mars
set point Az El

! flux calibration with a strong source neaby the targets
sou tmc1
@lincal-onoff.pako


!check your reference position wether there is emission on the reference position.
!@ref-onoff.pako



! C18O (2-1) and N2H+ (1-0) map
!------------------------------

! Do mapping of 1st TMC-1A, 2nd TMR1 and 3rd TMC1.
! Make 4 maps (each map takes about 30min, in total ~2hr)

@ otfmap-c18o-targetname
@ otfmap-c18o-targetname
@ otfmap-c18o-targetname
@ otfmap-c18o-targetname

! Make a pointing

@ pointing-mars
set point Az El
pause "Please enter the pointing corrections."

! Make 2 more maps

@ otfmap-c18o-targetname
@ otfmap-c18o-targetname
@ otfmap-c18o-targetname
@ otfmap-c18o-targetname
```
