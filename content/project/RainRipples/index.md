---
title: Rain ripples and puddle effect
summary: This project was completed during my internship in tencent games.For the project that i am working with, i realized the rain ripples and puddle effect,including puddles, flowing water, ripples of raindrops falling on the water surface and on a wet surface.
tags:
- Unity Shader


date: "2021-08-20T16:24:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:



links:

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.

---



I Realize the rain ripples and puddle effect ,including puddles, flowing water, ripples of raindrops falling on the water surface and on a wet surface.


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/RainRipples/2.png" >}}


Mask is used to control the scope of the water puddle; the water flow Wave uses two layers of wave normals to superimpose the flow; 


the water ripple uses the texture atlas to make the sequence frame animation, and the two layers of ripples are mixed; 

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/RainRipples/2.png" >}}


the raindrop effect uses the Voronoi algorithm to calculate the location of the raindrop , Sampling gradient map controls the appearance and disappearance. 


Use PBR shading in unity URP pipeline and PBR textures.


Shader parameter attributes:

1. Main Properties

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/RainRipples/2.png" >}}

Global Setting-XY-ZW: Control the Tiling and offset of all textures in Main Properties.

Color: The color of Albedo.

Invert Alpha: Whether to invert the A channel of the Albedo texture.

Albedo Color (Mask in A): Store Albedo Map. Channel A can be used to store the Mask or Smoothness Map of the puddle.

Saturation: Control the saturation or desaturation of the Albedo texture.

Brightness: Control the brightness of the Albedo texture.

Normal Map: Select the normal map to be used.

Normal Intensity: The unevenness of the Normal map.

Metallic Map (Smoothness A): Select the Metallic map to be used. The smoothness map is placed in the A channel.

Metallic: Metallic degree.

Smoothness: Smoothness.

Source: Select whether Smoothness is to use the image stored in the A channel of Albedo or Metallic.

Height Map: Select Height Map.
 
Height Scale: Control the degree of Height Map.

Ambient Occlusion Map: Select Ao map.

Ao Intensity: Control the degree of AO texture.

Emission Color: Specify the Emission color.
 
Emission Map: Select Emission Map.

Intensity: Emission degree.

2. Mask Properties : Mask attribute used to control the puddle

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/RainRipples/3.png" >}}

Visualize Mask: Whether to visualize the Mask.

Source: Whether to use Albedo A channel as an additional Mask.

Invert Mask: Whether to invert the A channel of the Detail Mask.

Detail Mask: Select a Detail Mask. If a map is not selected, it will be a black map. Black means no puddles.

Intensity: Control the level of detail in the puddle.

Contras: Control the black and white contrast ratio of the detail mask.

Spread: Control the range of puddles. It can be used as an animation to simulate the gradual increase of water in the rain puddle.

When spread is -1, the mask of the puddle is all white and becomes a water surface.

The larger the spread, the less water will become.

3. Reflection Properties


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/RainRipples/4.png" >}}


Color: Specify the color of the reflection.

Cubemap: Choose a cubemap.

Intensity: Control the intensity of reflections.

Blur: Specify the degree of blur.

Use Main Normal Map as Normal Direction:Whether to use the principal normal direction as the reflection direction. Used to simulate the effect of wet soil on the edge of a puddle when there is less water.


4. Rain Dots : this properties is used for raindrop effects on wet surfaces.

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/RainRipples/5.png" >}}

Gradient Tex: Control the visibility of raindrops, corresponding from left to right, the ones that have just fallen appear to disappear.

Intensity: Control the degree of visibility of raindrops.

Tiling: Tiling that controls raindrops.

Splash Speed: Control the speed of raindrops.

Size: Control the size of each raindrop.

5. Puddles Properties : this properties is used to control the properties of puddles.

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/RainRipples/6.png" >}}


Color: Specify the color of the puddle.

Use Main Base Color Map: Whether to use the main color (Albedo color) as the basic color of the puddle.

Base Color: The basic color of the puddle (Albedo color).

Saturation: Control the saturation or desaturation of the Albedo texture.

Brightness: Control the brightness of the Albedo texture. 

Blend Main Normal: Whether to blend Main Normal Map and Wave Normal Map.

Wave Normal Map: select Wave Normal Map

Main Wave: Whether to open Main Wave water flow

Intensity: The degree of unevenness of the Main Wave.

Speed: Main Wave moving speed.

Rotation: Main Wave flow direction angle.

Tiling: Tiling of Main Wave.

Detail Wave: Whether to enable the second layer of superimposed flow Detail Wave.

Intensity: The degree of unevenness of the Detail Wave.

Speed: Detail Wave movement speed.

Rotation: Detail Wave flow direction angle.

6. Rain Ripples : this properties control rain ripple properties


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/RainRipples/7.png" >}}

X(Columns)-Y(Rows)-Z(Speed)-W(Strart Frame)-Specify the number of columns and rows of the normal map of the selected texture atlas.

For example, the RainRipples 02_Atlas_Normal texture used by default is an atlas with 64 textures (64 cells = 8 columns x 8 rows).
The Z value represents the speed of the animation.
The value of W determines the start time. For example, the RainRipples 02_Atlas_Normal texture has 64 units. If the first frame = 0, then the last frame = 63.

Texture Atlas Normal: Select the texture atlas map. This can only be a normal map.

FlipBook Tiling: Specify Tiling.

Intensity: Controls the intensity of the texture normal.

Duplicate Texture Atlas: Enable the texture atlas normal of the second layer.

Intensity: the intensity of the normal of the second layer texture atlas

Scale: Control the size of the second layer texture atlas.

Rotate Details-Specify the rotation angle (degrees) of the copied texture atlas. By default, the copied texture will have the same coordinates as the first texture atlas. Change the rotation value to move the new texture atlas from its origin.

OffsetXY: Control the offset of the second layer texture atlas.

Distortion-Controls the degree of distortion caused by ripples. This attribute is associated with the basic color of the puddle attribute. If the Base color map of the puddle is not selected or if Use Main Albedo Map (Main Base Color) is enabled, the distortion level will not work.

Use Ao From Main Properties: Whether to use the AO amount in Main Properties to the puddle.

Use Emission From Main Properties: Whether to use the Emission amount in Main Properties to the puddle.




involved technology: Unity Shader、C#、shaderGUI()
