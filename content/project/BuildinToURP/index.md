---
title: Code migration from buildin pipeline to URP pipeline
summary: This project was finished during my internship at Tencent. I am mainly responsible for the porting of part of the shader code and the optimization of the original shader.
tags:
- Unity shader

date: "2021-06-10T16:24:00Z"

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



Assisting my mentor to carry out code transplantation for the project. During the period, I became familiar with the implementation of the character PBR skin and eyeballs and the framework architecture URP shader. I learned a series of URP usage and code framework example projects. At the same time, learn the low-level source code of unity URP and summarize it.




Participated in the completion of the transplantation of some codes, such as the transplantation of the CG to HLSL code of the eyeball part.




The original shader is optimized, and the switch and shader feature for multi-light source calculation and SH calculation are added to prevent the eyeball from being too dark due to Ambient Occlusion and make the effect more natural.




The Switch for the new shader feature:
{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/BuildinToURP/1.png" >}}




before And After:
{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/BuildinToURP/2.png" >}}

involved technology: C#、unity、Unity shader


