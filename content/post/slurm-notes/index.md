---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Slurm Notes"
subtitle: ""
summary: "Some notes on using slurm for HPC."
authors: []
tags: []
categories: []
date: 2021-10-20T00:20:45+10:00
lastmod: 2021-10-20T00:20:45+10:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
 
## Plot CPU hours used for jobs
The folowing creates a file `jobstats.txt` that contains the CPU time (seconds) for each job run bw the start+end time specified.
```bash
sacct -S 2021-01-01 -E 2021-10-06 -u avajpeyi -X -o "jobname%-40,cputimeraw" --parsable2 > jobstats.txt 
```
 
To plot the data you can use the following: 
{{< gist avivajpeyi 3beed78d92cd5f3520b4a1a93eb97cea >}}
  
{{< figure src="cpuhrs.png" title="Total CPU hours I've used ('19-'22) " lightbox="true" >}}
