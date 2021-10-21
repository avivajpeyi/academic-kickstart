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
 

## Interactive Jobs

If you want to test softwre that requires  GUI, MPI/Parallel/Multiple threads using interactive jobs may be useful.
Note that if you need a GUI -- you'll need to `ssh` with `-X`.

```bash
sinteractive --ntasks 1 --nodes 1 --time 00:30:00 --mem 32GB
```

Once you have obtained the resources and are in the interactive job session, you can open a `jupyter` notebook with the following:

1. Source envs
2. Setup tunnel + jupyter instance on cluster
    run:
    ```bash
    ipnport=$(shuf -i8000-9999 -n1)
    ipnip=$(hostname -i)
    echo "Run on local >>> ssh -N -L $ipnport:$ipnip:$ipnport avajpeyi@ozstar.swin.edu.au"
    jupyter-notebook --no-browser --port=$ipnport --ip=$ipnip
    ```

3. Local connection to interactive job
- run the command echoed above
- open the link to the jupyer notebook (also printed in the previous window)

4. Exit when done!

    Otherwise the job will keep running until it times out.
 
 
## Plot CPU hours used for jobs
The folowing creates a file `jobstats.txt` that contains the CPU time (seconds) for each job run bw the start+end time specified.
```bash
sacct -S 2021-01-01 -E 2021-10-06 -u avajpeyi -X -o "jobname%-40,cputimeraw" --parsable2 > jobstats.txt 
```
 
To plot the data you can use the following: 
{{< gist avivajpeyi 3beed78d92cd5f3520b4a1a93eb97cea >}}
  
{{< figure src="cpuhrs.png" title="Total CPU hours I've used ('19-'22) " lightbox="true" >}}



