# ColorKindness

A set of tools and resources to help people with reduced color perception

***

## So what is it?

As it turns out, and as it may or may not surprise you, computer accessibility tools for people with colorblindness *tend to suck.*

Most solutions (lms color shifting, daltonization, colorblind modes in games, etc.) all rely on the creator of a work to:

1. Care enough to alter their work and offer it alongside the original in the first place
2. Offer multiple versions of the altered work to support different kinds of reduced color perception
3. Implement each alteration correctly for every display technology and/or platform supported by the original

As most colorblind people can tell you, there's not much you can do if these criteria aren't met, and they often aren't met. There's no general purpose tool that solves this problem when the creator of a piece of media doesn't feel the need to help.

This project aims to correct that. For now, that's in the form of a dozen or so 3d-lookup tables (LUTs) that can be applied globally to windows displays (working on mac and linux, but they're a lot more involved)

Each folder contains files that can be applied using simple software that alters the color processing on your computer to better fit your range of vision. 

I've included the traditional alterations (LMS shifting and Daltonization) for the three types of dichromatic colorblindness, as well as some alternative corrections that aim to preserve as much of the original rendering intent as possible while enhancing readability. The latter were developed unscientifically, by asking colorblind people *what actually worked the best for them.*


## How do I use this repo?

`git clone` or download and extract the .zip file, pick the folder that matches your display technology's gamut and gamma (color range and luminance mapping) and load up the lut that works the best for your particular visual range. They're named according to different types of colorblindness (e.g. deuteranomaly = weak green, protanopia = red blind, etc. ) and then apply them to your display using [dwm_lut](https://github.com/lauralex/dwm_lut) or a similar program. If you're unsure what gamut/gamma to use, go with sRGB-2.2 

That's it, you should be good to go. If the one that should nominally work for you isn't great, play around with the other options or better yet, contact me, and I'll do my best to make one that does. The linear gamma LUTs can be used to make new LUTs for your own display, or as an intermediate transform in creative environments as reference.


## Testing Correction Effectiveness

If you aren't sure what kind of colorblindness you have, or have any form of anomolous trichromacy, you can load up a LUT and cycle through the Ishihara test plates provided in "Ishihara Positive Plates" in the test images folder. Use the LUT that allows you to see the most plates clearly. The traditional corrections may make it harder to see plates you normally don't have issues with when no correction is applied. The negative test plates are provided for reference only.

If multiple LUTs seem to work for you, or you don't want to sit through several slide shows to sus them out, try them on the color test patch image and pick the one you can easily differentiate the most squares on. 

## Limitations/Known Issues
Windows color management is in a pretty bad state right now, that's why I currently have to rely on third party software. I don't know that I'll be able to make it native on windows platforms for the forseeable future.

Some fullscreen games/applications will override your color settings. You can try setting these to borderless windowed, or converting the provided luts to .png format and loading them using [ReShade](https://github.com/crosire/reshade). I'm working on finding a consistent way to translate them into Reshade's supported format, but for now that's something you'll have to figure out.

The unscientific corrections work by shifting only the colors a person with anomolous trichromacy would have difficulty percieving into other ranges of the spectrum, compressing the full color gamut into a space they can see, while minimally altering the rest of the spectrum.

This concept is much the same as proofing a print for perceptual rendering from a digital image, or using a colorspace transform or tone mapping to work with footage in color grading or compositing software. This helps overcome the limitations inherent to the traditional correction methods for people with anomolous trichromacy while retaining the full range of colors they can still percieve. This also means that **if you have completely dichromatic vision, the unscientific corrections may not work very well for you.**

In addition, I have no one that can help me test Tritanomaly/Tritanopia at present, so I've provided two versions of the correction luts, one that shifts more of the spectrum toward cyan/green, and one that shifts more of the spectrum into magenta/red. They are labelled GP (green push) and MP (magenta push) respectively. I'd love feedback on which of these works best. 

The traditional correction methods shift the entire color space according to someone's color insensitivity, or alter contrast and saturation in certain color ranges to achieve better readability. While these work fine for people who have completely dichromatic vision, they're extreme for people with anomolous trichromatic vision, and wildly alter the appearance of media in a way many people with reduced color perception find unpleasant. The unscientific LUTS try to strike a middle-ground that works for as many people as possible, but for people with the more severe types of colorblindness, they may be the only effective option.

This project is also very early in development, so any input or collaboration is welcome. 


## Upcoming Improvements/To-Do

+  **Wide gamut/HDR/SMPTE profiles** -- I can generate luts for these, but I don't have any displays to validate the profiles on. Get in touch if you do
+  **ReShade Native LUTs** -- working on this.
+  **Corrections for monochromatic vision** -- This is a bit out of my depth, but if you have monochromatic vision and want to work with me on it, let me know.
+  **Support for mobile platforms** -- honestly have no idea where to start with this, it looks pretty fraught.
+  **Mac support** -- OSX is a fully color managed platform, so in theory, getting display color transforms to work should be straightforward. However, authoring synthetic ICC profiles is anything but. (and I don't own a mac) -- if you have reduced color perception, own a mac, and have some time and patience to spare, get in touch.
+  **Linux support** -- Same situation as above, except there's no guarantee it'll work on your machine. Linux color management depends entirely on your system environment. With multiple monitors and in some desktop environments, the best you can hope for is color-aware applications (firefox, krita, etc.) working consistently, not the whole UI, and if you use wayland I wouldn't hold my breath. May be achievable with vkbasalt or drm/dri hacks but I can't promise anything. Let me know if you have any ideas.
