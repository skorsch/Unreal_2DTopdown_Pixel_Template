# Unreal Engine 2D-Topdown Pixel Art Template 

Since Unreal is generally geared towards 3D games with complex graphics I've decided to make a 2D topdown template for a pixel art game. I've done this to help me achieve three goals:
1. Learn Unreal Engine
2. Create a base that I can use to continue making a game with (or multiple games)
3. To provide a starting point for others to use as well

I may add more to this template as I continue developing my game. (This was copied over from my private game repository)

# Project Overview

![Project Example Gif](/Examples/example.gif)

Pixel art generally requires use of the Paper2D plugin and to start I heavily referenced the [Unreal Docs](https://docs.unrealengine.com/5.0/en-US/paper-2d-in-unreal-engine/)

## Art

Quickly threw together some rough sprites I had already made (16x16 tiles).

## Accurate Representation of Pixel Art

There's a bunch of project settings that you have to turn off/change in order for sprite rendering to be correct:
- Motion blue = off
- Anti-aliasing = none
- Auto exposure = off, auto exposure bias = 0
- Dynamic global illumination = off
- Reflection method = none
- Shadow map method = shadow maps
- Ambient occlusion = off, ambient occlusion static fraction = off

At this point the level still looks different between the unlit and lit view so we have to add a post processing volume to each level to zero out any defaults:
- Infinte (unbound) = true
- Min EV100, max EV100 = 0
- Vignette intensity = 0
- Expand gamut = 0
- Tone curve = 0

Reference - [How to make a 2D Game in Unreal Engine 5 - 2024 Beginner Tutorial](https://youtu.be/QVxK2dPJr4g?t=1208)

## Dynamic Orthographic Camera

To prevent pixel distortion at different screen sizes/ratios I made the cameras ortho width change depending on viewport size. This means more of the map is revealed when you increase the viewport rather than scaling the pixels.

## Pixel Perfect Materials + Camera

Since I wanted to avoid situations where pixels weren't lined up with eachother I added the following:
- Created materials that 'snap' to the 'pixel grid'
- Adjusted sprite positions to match with pixel grid
- Moved camera along the pixel grid to reduce jittering

Reference - [How to make PIXEL PERFECT 2D Games with Unreal Engine 5](https://www.youtube.com/watch?v=0bbImg0T4VY) (although there was a slight bug in this implementation that I fixed by splitting up a calculation into its parts)

## Sprite Sorting 

Tilemaps don't support sprite sorting so to allow characters to walk 'in front of' and 'behind' different objects like walls etc. they have to be actors in the level rather than a tilemap. This slows down the level design process but may have been done anyways due to other features - such as the ability for walls to disappear if a character walks 'under' them (so players can see the tiles underneath.)
