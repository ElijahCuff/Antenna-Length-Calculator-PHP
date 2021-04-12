# Antenna Length Calculator

Advanced Dipole Antenna Length Calculator using PHP to perform simple math - designed to combat the issue of material selection on most calculators using material velocity factor ( VOP) 
   
// Inspired By this video on YouTube from Hak5 - https://m.youtube.com/watch?v=zMoKs1eiyO4

```
   
<?php
//
// Dipole Antenna Length Calculator
//
// Target Kilohertz
$khz = null;
//
// Material Velocity Factor ( Example, RG6 Coax Cable is around 0.85 ) 
$vop = null;
//
// Wavelength Target ( Example, for Half-Wave Antenna - you'd Split ( Divide ) the wavelength by 2 )
$split = null;
//
// Example URL = https://kyrosmo.ml/dipole.php?khz=1090&vop=0.85&split=2
//

if(($khz = $_REQUEST['khz']) != null){}
else
{
$khz = 1090;
}

if(($vop = $_REQUEST['vop']) != null){}
else
{
$vop = 1;
}

if(($split = $_REQUEST['split']) != null){}
else
{
$split = 1;
}


echo getDipoleLength($khz,$vop, $split);


function getDipoleLength($khz,$vop, $split)
{
  $speedOfLightToC = 299792458/1000000;
  $waveLength = $speedOfLightToC/$khz*1000;
  $dipoleFullWaveMM = $waveLength*$vop;

 $target =  $dipoleFullWaveMM/$split;
 $rounded = number_format((float)$target, 2, '.', '');
 return $rounded." millimetres";
}

?>
   

```
