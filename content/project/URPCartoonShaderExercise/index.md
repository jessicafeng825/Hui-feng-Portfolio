---
title: URP Cartoon character shader exercise
summary: This project mainly implements the character outline, cel shading, and multi-light source shadow of character cartoon rendering under the URP pipeline.
tags:
- Computer Graphics
- Unity Shader
date: "2021-03-03T16:24:00Z"

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


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/URPCartoonShaderExercise/cartoon1.png" title="URP Cartoon character shader exercise" >}}

### [👉 Click here to watch the video about it 👈](https://v.youku.com/v_show/id_XNTEzNjUzMTQ2NA==.html)


involved technology: C#、URP、HLSL

Use the external expansion method to outline, control the width of the outline according to the character's Z value and the camera's fov value, and the Z offset value to eliminate some unnecessary outlining weight and outline thickness attributes.

The first-order Cel shading is used to set the shadow's cut-off threshold, and NdotL controls the light. At the same time, use smoothstep function and variables to control the softness and hardness of the shadow.

Traverse multiple light sources and calculate all lighting effects, including self-illumination, indirect light and direct light; the realization of the shadow is to use ApplyShadowBias() function in the ShadowCaster pass to obtain the special clipping space coordinates for shadow projection, and the Z reverse processing is also required.

