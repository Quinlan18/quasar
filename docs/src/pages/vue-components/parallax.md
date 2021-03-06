---
title: QParallax
---

Parallax scrolling is a technique in computer graphics and web design, where background images move by the camera slower than foreground images, creating an illusion of depth in a 2D scene and adding to the immersion.

QParallax takes care of a lot of quirks, including image/video size which can actually be smaller than the window width/height.

## Installation
<doc-installation components="QParallax" />

## Usage

<doc-example title="Image background" file="QParallax/Image" />

::: warning
On some iOS platforms there may be problems regarding the autoplay feature of the native `<video>` tag. [Reference](https://webkit.org/blog/6784/new-video-policies-for-ios/). QParallax and Quasar are not interfering in any way with the client browser's ability/restrictions on the `<video>` tag.
:::

<doc-example title="Custom height with video background" file="QParallax/Video" />

<doc-example title="Custom speed" file="QParallax/Speed" />

<doc-example title="Scoped Slot" file="QParallax/ScopedSlot" />

## API
<doc-api file="QParallax" />
