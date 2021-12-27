---
title: Interactive snow Effect with footprints and tracks
summary: This project was finished during my internship in tencent games. For the game project that i was working with to achieve the needs of the dynamic interactive snow effect of the characters stepping on the snow, mainly the realization of snow material rendering, trajectory and footprints.
tags:
- Unity Shader
- Computer Graphics

date: "2021-08-10T16:24:00Z"

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

### [👉 Click here to watch the video about it 👈](https://www.youtube.com/watch?v=54g3fXiRKcg)

The dynamic interactive snow effect includes the rendering of snow material and the dynamic update of footprints or trajectories. This project is developed under the unity build-in pipeline.


1. Rendering of the Snow


The Snow is using PBR shaing and PBR textures,including Albedo, Normal, Metallic, Roughness, Ambient Occlusion, Emission Maps. What's more , Metallic, Roughness, Ambient Occlusion, Emission Maps are compressed into one picture, respectively in the RGBA channel.

When rendering snow, it is divided into upper snow and lower snow materials to be rendered separately, and then blend them.

This picture is the shader property panel of Snow：
{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/1.jpg" >}}


2.Updating the displacement texture

Place an orthogonal camera under the snow to shoot from bottom to top, use a material with a replacement shader to record and accumulate depth in each frame, set up shadertags for two different objects (Eg.ground and people), depending on the different shader tag to record different object depths.



Set the replacement shader to update the depth map and output a Displacement Render Texture. At the same time, use a height map to control the initial height of the snow, and at the same time as the initial value of the Displacement Render Texture.



{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/3.jpg" >}}



Perform vertex offset and change the Normal Map of the snow material according to Displacement RT. 



Set the surface subdivision parameters, perform mesh subdivision, and rewrite the surface subdivision function. This is used in the Build-in shader to increase model details. At the same time, a smoothing algorithm is used to smooth the area between the upper and the bottom.

The algorithm use the difference between the average of the surrounding texel with the current pixel to lerp between them to achieve the smoothing.






involved technology: Unity Shader、C#
