# gnome-shell-adaptived

Mojave introduces the concept of a dynamic desktop. Some of the things implemented here are health oriented.

* Dyanmic Wallpapers that change with time of day
  * Gnome does this `/usr/share/backgrounds/gnome`
* System wide dark mode
  * Gnome does this, however it is not implemented in many themes.
  * Application support is improving with this as they use newer gtk libs
  * I will need to look into the gtk architecture as I scale this up
* Dark resources are masked using gamma levels from the current background
  * This eleminates the issues of greys not *ever* looking uniform between gnome shell themes
  * According to the patrickcoffey blog I can override .css elements for the shell using this. I could in theory fork most of the default shell theme for dark mode and use an extension to modify the grey.

This is an effort to create a content aware dark mode for gnome.

## Research

* Some notes on Gnome Shell themes [here](http://www.patrickcoffey.io/post/theming-gnome-shell-sass-and-gulp). Likely depreciated.
* gnome-shell theme elements are now part of gtk-3.0.`/usr/share/themes/Aadwaita/gtk-3.0/gtk.css`
* 

### What is done in Mojave? (Chark full of new features)

[6:24: Opposite Visual Cues](https://developer.apple.com/videos/play/wwdc2018/210)

* Button click states now lighten when active in dark mode
* Group boxes are almost the same color however 'illuminate' their `border-radius` so as to introduce the depth needed in dark mode
* Shadows are modified see shadows

9:54 Dark-Mode is Content Focused
Application design uses light elements carefully so as not to distract focus from content.

Mail offers an option. It would be nice to add a background option to geary to or even have it pull gnome or gtk's css color setting.

### Desktop Tinting (10:00)
Implemneting Desktop Tinting should be the majority of the work in this project.

1. Take sample of desktop portion that is behind the window (mutter/gtk)
2. Derive average color for that x/y area
3. Blend that average color with the dark-mode gray (css/js?)
4. This final gray is used as the window-background property (css)
5. Controls inherit some of this themeing because they do not use a full 100% opacity. This enables some of the tinted colors to leech into their blacks, grays, and whites. (gtk/css?)


### Shadows (8:30)
2 Shadows, diffused-shadow and rim-shadow

* Rim shadow in dark mode is slightly crisper and higher (z index and contast / blur radius)
* Stroke is added to the inner rim of the rim-shadow so that the window has more definition above its shadows
