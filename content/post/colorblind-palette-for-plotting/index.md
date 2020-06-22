---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Colorblind Palette for Plotting"
subtitle: ""
summary: "Choosing colors is a pain. This snippet helps choose colors."
authors: []
tags: []
categories: []
date: 2020-06-19T00:20:45+10:00
lastmod: 2020-06-19T00:20:45+10:00
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
```python
from typing import List, Optional
import seaborn as sns

def get_colors(num_colors: int, alpha: Optional[float]=1) -> List[List[float]]:
    """Get a list of colorblind colors,

    :param num_colors: Number of colors.
    :param alpha: The transparency
    :return: List of colors. Each color is a list of [r, g, b, alpha].
    """
    cs = sns.color_palette(palette="colorblind", n_colors=num_colors)
    cs = [list(c) for c in cs]
    for i in range(len(cs)):
        cs[i].append(alpha)
    return cs

```
