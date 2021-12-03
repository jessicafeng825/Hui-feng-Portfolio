---
title: Large-scale water body rendering based on offline FFT.
summary: This project adopts offline FFT method, uses compute shader to calculate FFT waveform, and pre-computes and renders a series of displacement,Normal, bubble map, load resources dynamically at runtime. For water coloring, the unity shader under the default pipeline is used to realize the water effect of gradation, refraction, reflection, wave tip foam and shore waves.
tags:
- Computer Graphics
date: "2016-04-27T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Photo by rawpixel on Unsplash
  focal_point: Smart

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

### [❤️ Click here to watch the video about the water shader ❤️](https://v.youku.com/v_show/id_XNTEzNTA5MjgxMg==.html)
involved technology: C#、Unity shader、compute shader
This method was first used by the Assassin's Creed 3 team.
{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/offlinewaterShader/map3.jpg" title=" Assassin's Creed 3 " >}}

The FFT ocean structure uses the Tessendorf Spectrum+Donelan-Banner+stockham FFT algorithm architecture, and Implemented on the compute shader. 

{{< figure src="https://github.com/jessicafeng825/Hui-feng-Portfolio/blob/master/content/project/offlinewaterShader/map7.jpg" title="IDFT ocean Tessendorf from Simulating Ocean Water Jerry Tessendorf" >}}

The shape of the water body, the lighting effect, and the foam on the top of the wave are realized through the calculated displacement, normal, and bubble map.

{{< figure src="https://github.com/jessicafeng825/Hui-feng-Portfolio/blob/master/content/project/offlinewaterShader/map1.jpg" title="Ocean Surface Simulation NIVIDA" >}}
{{< figure src="https://github.com/jessicafeng825/Hui-feng-Portfolio/blob/master/content/project/offlinewaterShader/map2.jpg" title="Ocean Surface Simulation NIVIDA" >}}

Save the calculated Render Texture as png for each frame; use Resources.load() to load the texture into the array for dynamic loading,Then change the corresponding texture in the material according to the time.


{{< figure src="https://github.com/jessicafeng825/Hui-feng-Portfolio/blob/master/content/project/offlinewaterShader/map4.jpg" >}}
{{< figure src="https://github.com/jessicafeng825/Hui-feng-Portfolio/blob/master/content/project/offlinewaterShader/map5.jpg"  >}}
{{< figure src="https://github.com/jessicafeng825/Hui-feng-Portfolio/blob/master/content/project/offlinewaterShader/map6.jpg"  >}}

Here they baked a 32*32 resolution displacement map and a 128*128 normal map, baking a total of 128 frames. In the actual project, they found that a lower resolution of the displacement map would not have much impact. Here I use the compute shader to pre-calculate the texture data of the displacement map, normal map, and bubble map of 128 frames per frame, bake and save the data, and then load it into the shader for rendering when it runs. For the convenience of testing, I set the resolution to 512*512 first, but I can actually adjust it later.

This method requires a certain amount of memory to make the sequence frame, but it does not take up a lot of memory (it can be adjusted by setting the baked texture size and the sequence frame rate).

The realization of reflection and refraction obtains the corresponding reflection and refraction RenderTexture through the newly added camera in the screen space and transmits it to the water surface material.

### [❤️ Click here to watch the video about the implementation of the offline FFT with the Wave foam on the shore ❤️](https://v.youku.com/v_show/id_XNTEzNTk5NDEwMA==.html?spm=a2hbt.13141534.1_2.d_2&scm=20140719.manual.114461.video_XNTEzNTk5NDEwMA==)

The gradient of the ocean obtains the water depth by sampling the camera depth and the depth of the water surface, and then sampling the ramp map to construct the basic water color; the shore waves are constructed by obtaining the water depth . and use this way to achieve UV animation.


### [Zhihu Link with more detailed information about this project](https://zhuanlan.zhihu.com/p/351455975)

