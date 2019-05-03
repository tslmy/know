---
description: Think of heatmaps as disposable coffee trays.
---

# ☕ Explaining Heatmap Estimation with CNN, Metaphorically

Think of heatmaps as disposable coffee trays -- they are roughly planar, but at several parts they are pressed downwards.

![](https://piazza.com/redirect/s3?bucket=uploads&prefix=attach%2Fjqv6ndln63422n%2Fj6e0q77scir2gi%2Fjv889fqg9ru8%2F1200pxMcDonalds_Molded_Pulp_Drink_Tray_Top.jpg)![](https://piazza.com/redirect/s3?bucket=uploads&prefix=attach%2Fjqv6ndln63422n%2Fj6e0q77scir2gi%2Fjv88bfd0b5f4%2F1200pxMcDonalds_Molded_Pulp_Drink_Tray_Top.jpg)

Imagine that the [hourglass model](https://medium.com/@sunnerli/simple-introduction-about-hourglass-like-model-11ee7c30138) is a [_black box_](https://en.wikipedia.org/wiki/Black_box) that manufactures arbitrarily-shaped heatmaps/trays.

From real-life experience, you know what happens when you stack two differently-shaped trays -- they don't fit. When stacked trays don't fit, they appear taller than if they had fitted.

Well, the optimizer \(in PyTorch\) evaluates just that. Think of the optimizer as a ruler that repeatedly measures the height of the manufactured tray with a standard tray \(i.e. _ground truth_\), telling the tray-manufacturing blackbox: _yo, this tray was bad. Try again._

The black box will learn from the feedback, and adjust its products.

The cycle continues till the optimizer is satisfied, i.e., when the trays fit each other good enough.

