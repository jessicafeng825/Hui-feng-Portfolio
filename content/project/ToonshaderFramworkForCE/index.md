---
title: Toon shader framework for character and environment
summary: This project was completed during my internship in tencent games. it is also a trianing assignment for shader framework. At the same time, i need to build the shader framework, complete the demo containing the environment and the character, and package it to the mobile phone to run.
tags:
- Unity Shader
- Computer Graphics

date: "2021-07-10T16:24:00Z"

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



### [👉 Click here to watch the video about it 👈](https://studio.youtube.com/video/t1ZkP-FN5NA/edit)


The rendering framework is the PBR Toon shader under the unity URP pipeline. Refer to the URP lighting model and use BRDF based on Minimalist CookTorrance.SPR Batch Compatible.


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/1.jpg" >}}


the phone i am using for testing the performance is OPPO findX2 which has  Qualcomm 585 CPU and Adreno 650 GPU with Android OS 10 system. here is some picture of the performance:

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/2.jpg" >}}

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/3.jpg" >}}

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/4.jpg" >}}

the fps is around 60.

1. shader property


The objects in the environment and the character will use the same shader as follow:


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/7.jpg" >}}


2. surface option


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/8.png" >}}


Workflow Mode : Specular or Metallic

SurfaceType : Opaque or Transparent

Render Face : Front Back Both (For Forward Pass)

Alpha Clipping : enable the Alpha Clipping or not


3. Base Map


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/9.png" >}}


The input of the basic texture,Albedo ,Normal and AO. 

Albedo and AO merge channels into one texture for input.

Emission input a single texture.


4. Shadow


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/10.png" >}}


This is about the setting options for shadows. You can choose whether to use the ramp map as the shadow. If not, use the universal Toon rendering calculation method which is  NdotL+2 line. And use Two thresholds control the dividing line.


UseRampMapShadow : Use RampMap to control shadow attenuation.

VOffset : V coordinate sampled by RampMap

Shadow1Color ：The first layer of shadow color

Shadow2Color ：Second layer shadow color

Shadow1Step : First layer shadow threshold

Shadow1Feather : The first layer of shadow feathering value

Shadow2Step : Second layer shadow threshold

Shadow2Feather : The second layer of shadow feathering value

EnableInShadowMap : Enable InshadowMap or not. inShadowMap is the fixed shadow map.

Receive Shadow : Receive Shadow or not


5. Specular


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/11.png" >}}


This is about the Specular setting options. Merge normal map and Metal Smooth map. Take the normal map RG channel, Metal and Smooth each occupy a channel to merge into one texture. The normal calculation uses the RG channel to calculate the Z channel result. 


You can choose whether it is the Specular rendering of the hair. If it is, the anisotropic hair Specular map will be sampled. If not, the GGX Specular item will be used for regular PBR calculation.


SpecularStep : Specular threshold

SpecularFeather : Specular feathering

Smoothness : Smoothness 

HairSpecular : Use anisotropic hair Specular map or not

HairShiftMap : Tangent offset graph, offset intensity

SpecularShift : The first layer of Specular offset

SpecularShiftSec : The second layer of Specular offset

SpecularSecMul : The second layer of Specular intensity（*Specular)

EnablesSpecularHighlights : Use specular or not


6. Rim And Outline


Outline option use the normal expansion algorithm, and use the SmoothOutline algorithm to smooth the stroke.


{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/12.png" >}}


OpenRim : Enable Rim Light or Not


EnableOutline ：Enable Outline or not

UseSmoothNormal : Enable Smooth Outline or not. the algorithm using is from here:https://github.com/Jason-Ma-233/JasonMaToonRenderPipeline#%E5%B9%B3%E6%BB%91%E6%B3%95%E7%BA%BF%E5%AF%BC%E5%85%A5%E5%B7%A5%E5%85%B7ModelOutlineImporter) 

OutlineColor:

OutlineWidth:


7.AdvancedOptions



{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/ToonshaderFramworkForCE/13.png" >}}


Environment Reflections : Enable refelction or not

Enable GPU Instancing : Enable GPU Instancing or not

RenderQueue : 渲染队列



involved technology: Unity Shader、Computer Graphics、ShaderGUI
