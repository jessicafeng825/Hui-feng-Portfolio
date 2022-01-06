---
title: Interactive snow Effect with footprints and tracks
summary: This project was finished during my internship in tencent games. For the game project that i was working with to achieve the needs of the dynamic interactive snow effect of the characters stepping on the snow, mainly the realization of snow material rendering, trajectory and footprints.
tags:
- Unity shader
- Computer Graphics

date: "2021-08-10T16:24:00Z"
authors: ["admin"]
featured: true
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

{{< hl >}}


{{< hl >}}
### involved technology: Unity Shader、C#、shaderGUI()

{{< youtube 54g3fXiRKcg >}}


The dynamic interactive snow effect includes **the rendering of snow material** and **the dynamic update of footprints or trajectories**. This project is developed under the unity build-in pipeline.
{{< hl >}}


{{< hl >}}

# Rendering of the Snow


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/3.jpg" >}}


The Snow is using **PBR shaing and PBR textures**,including Albedo, Normal, Metallic, Roughness, Ambient Occlusion, Emission Maps. 

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/4.png" >}}

What's more , Metallic, Roughness, Ambient Occlusion, Emission Maps are compressed into one picture, respectively in the RGBA channel.

When rendering snow, it is divided into **upper snow** and **lower snow materials** to be rendered separately, and then blend them.

This picture is the **shader property panel of Snow：**
{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/1.jpg" >}}

Also,use shaderGUI() to adjust the shader properties panel for ease of use by other artists.

{{< hl >}}


{{< hl >}}

# Updating the displacement texture

Place an **orthogonal camera** under the snow to shoot from bottom to top

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/5.png" >}}


At the same time, use a **heightmap** to control the initial height of the snow, and at the same time as the initial value of the Displacement Render Texture. use Blit() to blit with the initial heightmap to get the initial snow height.


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/6.png" >}}


use a material with a **replacement shader** to **_record and accumulate depth in each frame_** , set up **shadertags**  for two different objects (Eg.ground and people), depending on the different shader tag to record different object depths.

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/7.png" >}}

We create the two render texture we'll need each frame,RT1 and RT2. We will setup the **target texture** and pass the right target texture from camera to the shader **according to the flag(a bool variable)**. For Each frame we **swap the target texture to always keep the result of the shader.**

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/8.png" >}}

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/9.png" >}}

after rendering (in the OnPostRender() function)we will use **blit() to blit the first RT in the second RT to get the tracks depth texture and switch the flag.**

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/10.png" >}}


Set the replacement shader to update the **depth map** and output a **Displacement Render Texture** and then calculate the new height in the ReciveDepth.shader file which will be using as replacement shader.

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/11.png" >}}


Perform **vertex offset and change the Normal Map** of the snow material according to Displacement RT in the material render shader.

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/12.png" >}}

Set the surface **subdivision parameters**, perform **mesh subdivision**, and rewrite the surface subdivision function. This is used in the Build-in shader to increase model details.(this will be perfromed in the material render shader)

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/13.png" >}}

At the same time, a smoothing algorithm is used to smooth the area between the upper and the bottom.The algorithm use the difference between the average of the surrounding texel with the current pixel to lerp between them to achieve the smoothing.(this will be perfromed in the replacement shader while we are calculating the height map)

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/14.png" >}}

Perfrom PBR Lighting calculation in vert and frag in the material render shader.

Part of the code AS show：

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/15.png" >}}
{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/SnowTesselation/16.png" >}}



