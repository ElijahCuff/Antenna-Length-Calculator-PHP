# Antenna Length Calculator

Advanced Dipole Antenna Length Calculator using PHP to perform simple math - designed to combat the issue of material selection on most calculators using material velocity factor ( VOP) 
   
// Inspired By this video on YouTube from Hak5 - https://m.youtube.com/watch?v=zMoKs1eiyO4
  
  
Example usage,      
https://kyrosmo.ml/dipole.php?mhz=1090&vf=0.85&split=2
```
   
<?php
//
// Dipole Antenna Length Calculator
//
// Target megahertz 
$mhz = null;
//
// Material Velocity Factor ( Example, RG6 Coax Cable is around 0.85 using 116 mm node spacing for 1090Mhz target frequency ) 
$vf = null;
//
// Wavelength Target ( Example, for Half-Wave Antenna - you'd Split ( Divide ) the wavelength by 2 )
$split = null;
//
// Example URL = https://kyrosmo.ml/dipole.php?mhz=1090&vop=0.85&split=2
//

if(($mhz = $_REQUEST['mhz']) != null){}
else
{
$mhz = 1090;
}

if(($vf = $_REQUEST['vf']) != null){}
else
{
$vf = 1;
}

if(($split = $_REQUEST['split']) != null){}
else
{
$split = 1;
}


echo getDipoleLength($mhz,$vf, $split);

// Get Velocity from Node Spacing millimetres and Mhz Target  
//echo getVelocityFactor(200, $mhz);

function getDipoleLength($mhz,$vf, $split)
{
  $C = 299792458/1000000;
  $waveLength = ((($C/$mhz)*1000)*$vf)/$split;

$forNo = number_format((float)$waveLength, 2, '.', '');
$end = "mm";
if($waveLength >= 100)
{
  $forNo = number_format((float)$waveLength/10, 2, '.', '');
  $end = "cm";
}

if($waveLength >= 1000)
{
  $forNo = number_format((float)$waveLength/1000, 2, '.', '');
  $end = "m";
}

 return $forNo." ".$end;
}


function getVelocityFactor($nodeSpacingMM, $FrequencyMhz)
{
$speedOfLightToC = 299792458/1000000;
$spV = $speedOfLightToC*1000/2/$FrequencyMhz;
$vf =  $nodeSpacingMM/$spV;
return $vf;
}

?>

   

```
