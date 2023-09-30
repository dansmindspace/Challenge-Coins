# The Coding Train - Challenge Coin

This challenge coin was designed as part of The Coding Trains Logo Variations Repository for Hacktoberfest.

![The Coding Train - Challenge Coin Rotating GIF](https://github.com/dansmindspace/Challenge-Coins/blob/656f0e0afdb561f0acc0b933e2d47c0a5af0802c/The%20Coding%20Train/CodingTrainChallengeCoin.gif)

## The SCAD

    //Coding Train Challenge Coin
    //Author: Dan TheLostSorcerer
    //GitHub: dansmindspace
    //Website: https://dansmind.space
    
    //Thickness of the coin in mm.
    coin_thickness=5;
    //Diameter of the coin in mm.
    coin_diameter=76;
    //Depth of the inset faces in mm.
    coin_inset=1.5;
    //Year to print on coin.
    coin_year="2023"; //6
    
    /* [Hidden] */
    $fa=5;
    $fs=0.4;
    omega = 0.1;
    
    //Coding Train Colors
    purple="#70327E";
    blue="#30C5F3";
    pink="#EF63A4";
    yellow="#F89E4F";
    
    //For animating the coin
    $vpr = [0, 360 * $t, 0];
    
    module challengeCoin(w, h) {
        union() {
            difference() {
                //Coin Body
                cylinder(h=h, d=coin_diameter);
                //Top Inset
                translate([0,0,h - coin_inset])
                    cylinder(h=coin_inset + omega, d=coin_diameter- 2*w);
                //Bottom Inset
                translate([0,0,-omega])
                    cylinder(h=coin_inset + omega, d=coin_diameter- 2*w);
            }
            
            //Scale the logo to fit
            scale([0.20,0.20,1])
                //Center Logo
                translate([-120,-105,0])
                    codingTrainLogo(8, h);
                    
            text_font="Courier New; Style = Bold";
            //Text Top
            translate([0,-30,coin_inset+omega])
                linear_extrude(h - coin_inset-omega)
                    text(text=coin_year, size=5, halign="center", font=text_font);
            translate([0,25,coin_inset+omega])
                linear_extrude(h - coin_inset-omega)
                    text(text="The", size=5, halign="center", font=text_font);
            translate([0,18,coin_inset+omega])
                linear_extrude(h - coin_inset-omega)
                    text(text="Coding Train", size=5, halign="center", font=text_font);
            
            //Text Bottom
            translate([0,-30,0])
                linear_extrude(coin_inset+omega)
                    mirror([1,0,0])
                        text(text=coin_year, size=5, halign="center", font=text_font);
            translate([0,25,0])
                linear_extrude(coin_inset+omega)
                    mirror([1,0,0])
                        text(text="The", halign="center", size=5, font=text_font);
            translate([0,18,0])
                linear_extrude(coin_inset+omega)
                    mirror([1,0,0])
                        text(text="Coding Train", halign="center", size=5, font=text_font);
        }
    }
    
    module codingTrainLogo(w, h) {
    //Back Wheel
    wheel([75,60,0], 53 * 2, w, h, purple);
    
    //Top
    roundedLine([30,105,0], 41, w, h, 90, purple);
    roundedLine([30,146,0], 13, w, h, 180, purple);
    roundedLine([17,146,0], 25, w, h, 90, purple);
    roundedLine([17,171,0], 108, w, h, 0, purple);
    roundedLine([125,171,0], 46, w, h, -90, purple);
    
    //Smokestack
    roundedLine([145,171,0], 51, w, h, 0, blue);
    roundedLine([145,171,0], 46.5, w, h, -90 + 8.5, blue);
    roundedLine([196,171,0], 46.5, w, h, -90 - 8.5, blue);
    
    //Engine
    roundedLine([151,108,0], 35, w, h, -90, yellow);
    roundedLine([171,108,0], 35, w, h, -90, yellow);
    roundedLine([191,108,0], 35, w, h, -90, yellow);
    roundedLine([149,53,0], 45, w, h, 0, yellow);
    
    //Front Wheels
    wheel([150,25,0], 18 * 2, w, h, blue);
    wheel([190,25,0], 18 * 2, w, h, blue);
    
    //Front Plate
    roundedLine([205,53,0], 38, w, h, -90 + 35, pink);
    roundedLine([205,53,0], 38, w, h, 90 - 35, pink);
    roundedLine([227,85,0], 38, w, h, 90 + 35, pink);
    
    }
    
    module wheel(origin, diameter, thickness, height, colour=undef) {
    color(colour)
    translate(origin)
        difference(){
            cylinder(h = height, d = diameter);
            translate([0,0,-omega])
                color(undef)
                    cylinder(h = height + 2 * omega, d = diameter - thickness * 2);
        }
    };
    
    module roundedLine(origin, length, width, height, angle, colour=undef) {
        color(colour)
        translate(origin)
            rotate([0,0,angle])
                union() {
                    cylinder(h = height, d = width);
                    translate([0, -width / 2, 0])
                        cube([length, width, height]);
                    translate([length, 0, 0])
                        cylinder(h = height, d = width);
                }
    };
    
    challengeCoin(3, coin_thickness);


[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg
