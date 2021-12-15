---
title: Overdraw rate analysis and debugging tool
summary: This project is a tool forr showing the overdraw rate both in Unity Editor and in running Game. it realized the display of the overdraw-related indicators of each camera during the debugging of the mobile game, so as to detect and troubleshoot the overdraw problem in the mobile game.
tags:
- Tools

date: "2020-11-10T16:24:00Z"

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

In order to detect where the overdraw rate is relatively high, I developed this tool. This tool can display the overdraw rate when running in the unity editor, and it can also display the overdraw rate when the game is running in the Android platfrom. by using this tool, you can find out Where is the performance bottleneck of the game.

### [👉 Click here to read the detailed Description about it 👈](https://github.com/jessicafeng825/Hui-feng-Portfolio/blob/master/content/project/OverwriteTools/overdraw%E6%8C%87%E6%A0%87%E5%B7%A5%E5%85%B7%E4%BB%8B%E7%BB%8D.pptx?raw=true)
### [👉 Here is my article on how to implement this tool. 👈](https://zhuanlan.zhihu.com/p/323421079)

involved technology: C#、Unity shader、OnGUI()、compute shader

Perform a high-precision sampling for each camera below the scene, and use the replacement shader to normalize the sampling texture and save it as a Render Texture.

Use the Compute shader to use the Parallel reduction algorithm to calculate the number of times each pixel is drawn which is using the parallel computing, and pass it back to C# for the statistics of Overdraw.
compute shader is used to add up all the pixels in the overdrawTexture and stores the information into this component.

Use OnGUI() function to count the peak value of single frame fillrate multiple, single frame fillrate multiple, GPU actual fillrate multiple, GPU fillrate multiple peak and actual fillrate multiple, and output the display.

{{< figure src="https://raw.githubusercontent.com/jessicafeng825/Hui-feng-Portfolio/master/content/project/OverwriteTools/map1.jpg" >}}

the peak value of single frame fillrate multiple = the peak value of single frame fillrate/ frame rendering camera resolution

single frame fillrate multiple = single frame fillrate/ frame rendering camera resolution

GPU actual fillrate multiple = The total number of fills in this frame /screen resolution to which this frame is projected ;The higher the value, the greater the overdraw rate.

GPU fillrate multiple peak =  the peak of GPU actual fillrate multiple

actual fillrate multiple = Add the actual GPU fillrates multiples of all cameras .and also shows the maximum of actual fillrates.
