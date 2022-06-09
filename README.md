# NeoPop
Synth is CRED's inbuilt library for using Neumorphic components in your app.

What really is Neumorphism? It's an impressionistic style, playing with light, shadow, and depth to create a digital experience inspired by the physical world. That's the definition anyway. Our recommendation is you try it out to see what you make of it. If you do create something with Synth, let us know. We're excited to see where you take it.

A note for the curious: if you wish to learn more about Synth, we have a post detailing the concept and CRED's philosophy behind it [here](https://blog.cred.club/team-cred/design/world-meet-neumorphism-open-sourcing-our-ui-framework/).

For iOS, checkout [Synth-iOS](https://github.com/CRED-CLUB/synth-ios)

![Banner](https://i.imgur.com/tKZeAwO.png "Banner")

## Install
You can install synth by adding this to your build.gradle file:

```
dependencies {
  implementation 'club.cred.android:synth:1.0.0'
}
```

## Usage & SDK Limitations

To use synth, the parent layout which contains the synth views must specify:

```xml
android:clipChildren="false"
```

Synth renders neumorphic components only on devices running API 28 (Pie) or later. This is because Synth internally uses [`BlurMaskFilter`](https://developer.android.com/reference/android/graphics/BlurMaskFilter) to render shadows and highlights which are drawn outside of the view bounds — this allows you to align Synth views with other views easily.

The issue below API 28, is, to make `BlurMaskFilter` work, we need to use [hardware acceleration](https://developer.android.com/guide/topics/graphics/hardware-accel) on the view which causes the shadows and highlights to be clipped. We could solve for this by adding padding to the views (similar to how CardView does it) but chose not to because of alignment issues.

In lieu of this, we decided to introduce "compat" version of all our views which render a simple single colored background on the view on devices below API 28.

# PopLayout

## Plunk
![Soft Button](https://i.imgur.com/ih0WqFz.png "Soft Button")

PopLayout renders the elevated neumorphic platform on which the text is drawn. this elevated platform can be customized in two ways:
1. By specifying the button position as `bottom|right`, neopop will attempt to compute the all the surfaces of the popFrameLayout
```xml
<club.cred.neopop.PopFrameLayout
    ...
    android:clickable="true"
    app:neopop_button_position="bottom|right"
    app:neopop_center_surface_color="@color/white"
    app:neopop_depth="3dp"
    app:neopop_parent_view_color="@color/black"/>
```

## Flat
2. By specifying a complete appearance for all aspects of the elevated platform
```xml
<club.cred.neopop.PopFrameLayout  
    ...
    android:clickable="true" 
    app:neopop_parent_view_color="@color/black"
    app:neopop_button_position="center"  
    app:neopop_center_surface_color="@color/white"  
    app:neopop_depth="3dp"  
    />
```

## Shimmer
```xml
<club.cred.neopop.PopFrameLayout  
  ...
  app:neopop_shimmer_duration="5000"  
  app:neopop_shimmer_width="24dp"  
  app:neopop_shimmer_color="#f00"  
  app:neopop_show_shimmer="true"/>
  ```

## Flat Strokes

```xml
<club.cred.neopop.PopFrameLayout  
  ...
  app:neopop_button_position="center"  
  app:neopop_draw_full_height="true"  
  app:neopop_draw_full_width="true"  
  app:neopop_parent_view_color="@color/black"
  app:neopop_stroke_color="#f00">
```

## Plunk Strokes

```xml
<club.cred.neopop.PopFrameLayout  
  ...
  android:clickable="true"
  app:neopop_button_position="bottom|right"
  app:neopop_bottom_surface_color="#0f0"  
  app:neopop_right_surface_color="#0f0"
  app:neopop_top_surface_color="@android:color/transparent"  
  app:neopop_left_surface_color="@android:color/transparent"  
  app:neopop_is_stroked_button="true"  
  app:neopop_stroke_color="#0f0">
```

## Adjacent Buttons
```xml
<androidx.constraintlayout.widget.ConstraintLayout  
  android:layout_width="match_parent"  
  android:layout_height="200dp"  
  android:background="@color/white">  
  
	 <club.cred.neopop.PopFrameLayout  
	  android:id="@+id/b2"    
	  android:clickable="true"  
	  app:layout_constraintEnd_toEndOf="@id/view"  
	  app:layout_constraintTop_toTopOf="parent"  
	  app:layout_constraintBottom_toBottomOf="parent"  
	  app:neopop_button_position="center"  
	  app:neopop_draw_full_height="true"  
	  app:neopop_button_on_right="@id/b1"  
	  app:neopop_draw_full_width="true"  
	  app:neopop_center_surface_color="@color/black"  
	  app:neopop_parent_view_color="@color/white">
	   ...content   
	 </club.cred.neopop.PopFrameLayout>  
	 
	 <View  android:id="@+id/view"  
	  android:layout_width="3dp"  
	  android:layout_height="0dp"  
	  app:layout_constraintStart_toStartOf="@id/b1"  
	  app:layout_constraintTop_toTopOf="parent"  
	  app:layout_constraintBottom_toBottomOf="parent"/>  
	  
	 <club.cred.neopop.PopFrameLayout  
	  android:id="@+id/b1"  
	  android:clickable="true"  
	  app:neopop_button_on_left="@id/b2"  
	  app:layout_constraintBottom_toBottomOf="parent"  
	  app:layout_constraintEnd_toEndOf="parent"  
	  app:layout_constraintTop_toTopOf="parent"  
	  app:neopop_button_position="center"  
	  app:neopop_draw_full_height="true"  
	  app:neopop_draw_full_width="true"  
	  app:neopop_center_surface_color="#f00"  
	  app:neopop_parent_view_color="@color/white">  
	  ...content
	 </club.cred.neopop.PopFrameLayout>  
</androidx.constraintlayout.widget.ConstraintLayout>
```
## PopLayout All configs
```xml
<club.cred.neopop.PopFrameLayout  
  android:layout_width="match_parent"  
  android:layout_height="207dp"  
  app:neopop_center_surface_color="@color/white"  
  android:layout_marginHorizontal="24dp"  
  android:layout_marginVertical="54dp">  
  
	 <androidx.constraintlayout.widget.ConstraintLayout
	  android:layout_width="match_parent"  
	  android:layout_height="match_parent">  
	  
		 <club.cred.neopop.PopFrameLayout  
		  android:id="@+id/topLeft"  
		  android:layout_width="84dp"  
		  android:layout_height="53dp"  
		  app:neopop_center_surface_color="#f00"  
		  app:neopop_parent_view_color="@color/white"  
		  app:neopop_grandparent_view_color="@color/black"  
		  app:layout_constraintTop_toTopOf="parent"  
		  app:layout_constraintStart_toStartOf="parent"  
		  app:neopop_button_position="top|left"  
		  android:clickable="true"/>  
		  
		 <club.cred.neopop.PopFrameLayout  android:id="@+id/top"  
		  android:layout_width="84dp"  
		  android:layout_height="53dp"  
		  app:neopop_center_surface_color="#f00"  
		  app:neopop_parent_view_color="@color/white"  
		  app:neopop_grandparent_view_color="@color/black"  
		  app:layout_constraintTop_toTopOf="parent"  
		  app:layout_constraintStart_toStartOf="parent"  
		  app:layout_constraintEnd_toEndOf="parent"  
		  app:neopop_button_position="top"  
		  android:clickable="true"/>  
		  
		 <club.cred.neopop.PopFrameLayout  android:id="@+id/topRight"  
		  android:layout_width="84dp"  
		  android:layout_height="53dp"  
		  app:neopop_center_surface_color="#f00"  
		  app:neopop_parent_view_color="@color/white"  
		  app:neopop_grandparent_view_color="@color/black"  
		  app:layout_constraintTop_toTopOf="parent"  
		  app:layout_constraintEnd_toEndOf="parent"  
		  app:neopop_button_position="top|right"  
		  android:clickable="true"/>  
		  
		 <club.cred.neopop.PopFrameLayout  android:id="@+id/right"  
		  android:layout_width="84dp"  
		  android:layout_height="53dp"  
		  app:neopop_center_surface_color="#f00"  
		  app:neopop_parent_view_color="@color/white"  
		  app:neopop_grandparent_view_color="@color/black"  
		  app:layout_constraintTop_toTopOf="parent"  
		  app:layout_constraintBottom_toBottomOf="parent"  
		  app:layout_constraintEnd_toEndOf="parent"  
		  app:neopop_button_position="right"  
		  android:clickable="true"/>  
		  
		 <club.cred.neopop.PopFrameLayout  android:id="@+id/bottomRight"  
		  android:layout_width="84dp"  
		  android:layout_height="53dp"  
		  app:neopop_center_surface_color="#f00"  
		  app:neopop_parent_view_color="@color/white"  
		  app:neopop_grandparent_view_color="@color/black"  
		  app:layout_constraintBottom_toBottomOf="parent"  
		  app:layout_constraintEnd_toEndOf="parent"  
		  app:neopop_button_position="bottom|right"  
		  android:clickable="true"/>  
		  
		 <club.cred.neopop.PopFrameLayout  android:id="@+id/bottom"  
		  android:layout_width="84dp"  
		  android:layout_height="53dp"  
		  app:neopop_center_surface_color="#f00"  
		  app:neopop_parent_view_color="@color/white"  
		  app:neopop_grandparent_view_color="@color/black"  
		  app:layout_constraintBottom_toBottomOf="parent"  
		  app:layout_constraintEnd_toEndOf="parent"  
		  app:layout_constraintStart_toStartOf="parent"  
		  app:neopop_button_position="bottom"  
		  android:clickable="true"/>  
		  
		 <club.cred.neopop.PopFrameLayout  android:id="@+id/bottomLeft"  
		  android:layout_width="84dp"  
		  android:layout_height="53dp"  
		  app:neopop_center_surface_color="#f00"  
		  app:neopop_parent_view_color="@color/white"  
		  app:neopop_grandparent_view_color="@color/black"  
		  app:layout_constraintBottom_toBottomOf="parent"  
		  app:layout_constraintStart_toStartOf="parent"  
		  app:neopop_button_position="bottom|left"  
		  android:clickable="true"/>  
		  
		 <club.cred.neopop.PopFrameLayout  android:id="@+id/left"  
		  android:layout_width="84dp"  
		  android:layout_height="53dp"  
		  app:neopop_center_surface_color="#f00"  
		  app:neopop_parent_view_color="@color/white"  
		  app:neopop_grandparent_view_color="@color/black"  
		  app:layout_constraintBottom_toBottomOf="parent"  
		  app:layout_constraintTop_toTopOf="parent"  
		  app:layout_constraintStart_toStartOf="parent"  
		  app:neopop_button_position="left"  
		  android:clickable="true"/>  
		  
		 <club.cred.neopop.PopFrameLayout  android:id="@+id/center"  
		  android:layout_width="84dp"  
		  android:layout_height="53dp"  
		  app:neopop_center_surface_color="#f00"  
		  app:neopop_parent_view_color="@color/white"  
		  app:neopop_grandparent_view_color="@color/black"  
		  app:layout_constraintBottom_toBottomOf="parent"  
		  app:layout_constraintTop_toTopOf="parent"  
		  app:layout_constraintEnd_toEndOf="parent"  
		  app:layout_constraintStart_toStartOf="parent"  
		  app:neopop_button_position="center"  
		  android:clickable="true"/>  
	 </androidx.constraintlayout.widget.ConstraintLayout>  
</club.cred.neopop.PopFrameLayout>
```
# TiltLayout

## Non Floating
```xml
<club.cred.neopop.NeoPopQuadFrameLayout
		....  
	  android:clickable="true"  
	  app:neopop_parentViewColor="@color/black"  
	  app:neopop_black_shadow_height="15dp"  
	  app:neopop_black_shadow_top_padding="0dp"  
	  app:neopop_card_rotation="18.8"  
	  app:neopop_gravity="on_ground"
	  app:neopop_shadow_rotation="32"  
	  app:neopop_show_shimmer="false"/>
```

##  Floating
2. By specifying a complete appearance for all aspects of the flat surface
```xml
<club.cred.neopop.NeoPopQuadFrameLayout
		....  
	  android:clickable="true"  
	  app:neopop_parentViewColor="@color/black"  
	  app:neopop_black_shadow_height="15dp"  
	  app:neopop_black_shadow_top_padding="0dp"  
	  app:neopop_card_rotation="18.8"  
	  app:neopop_gravity="on_space"
	  app:neopop_shadow_rotation="32"  
	  app:neopop_show_shimmer="false"/>
```

## Shimmer

![Drawable Button](https://i.imgur.com/Bnjb5Cj.png "Drawable Button")

2. By specifying a complete appearance for all aspects of the icon pit
```xml
<club.cred.neopop.NeoPopQuadFrameLayout  
  ...
  app:neopop_shimmer_duration="5000"  
  app:neopop_top_shimmer_color="#f00"  
  app:neopop_bottom_shimmer_color="#0f0"  
  app:neopop_show_shimmer="true"  
  app:neopop_shadow_rotation="32">
```
## All button attributes
| Attribute | Description | Value |
|--|--|--|
|`app:neopop_depth`| depth of shadow | dimension |
|`app:neopop_top_surface_color` or `app:neopop_right_surface_color` or `app:neopop_bottom_surface_color` or `app:neopop_left_surface_olor`| shadow colors | color |
| `app:neopop_parent_view_color` | immediate ancestor's color | color |
| `app:neopop_grandparent_view_color` | 2nd level ancestor's color | color |
| `app:neopop_stroke_color` | layout's stroke colors | color |
| `app:neopop_surface_color` | card color | style resource |
| `app:neopop_is_top_surafce_visible` or `app:neopop_is_right_surface_visible` or `app:neopop_is_bottom_surface_visible` or `app:neopop_is_left_surface_visible`| shadow visibility | boolean |
| `app:neopop_button_position` | position of button in ref to parent view | `top`,`right`, `bottom`,`left`,`center` |
| `app:neopop_button_on_top` or `app:neopop_button_on_right` or `app:neopop_button_on_bottom` or `app:neopop_button_on_left`| assign reference of button which is on top/right/bottom/left of this button | view id |
| `app:neopop_shimmer_duration` | total duration of shimmer | seconds in millis |
| `app:neopop_shimmer_color` | shimmer color | color |
| `app:neopop_shimmer_width` | shimmer width | dimension |
| `app:neopop_show_shimmer` | enable shimmer | boolean |
| `app:neopop_shimmer_repeat_delay` | repeat delay between shimmers | seconds in millis|
|`app:neopop_shimmer_start_delay` | shimmer start delay | seconds in millis |
|`app:neopop_animate_on_touch` | use button animator internally to animate | boolean |
## Tilt Specific Attributes
| Attribute | Description | Value |
|--|--|--|
| `app:neopop_shadow_color` | bottom plane color | color |
| `app:neopop_card_rotation` |  |  |
| `app:neopop_shadow_rotation` |  |  |
| `app:neopop_gravity` | floating or static | `on_space`, `on_ground`|
| `app:neopop_top_shimmer_color` | top shimmer color  | color |
| `app:neopop_bottom_shimmer_color` | bottom shimmer color | color |
| `app:neopop_black_shadow_top_padding` | | |
| `app:neopop_black_shadow_height` |  | |
| `app:neopop_floating_shadow_color` | | color |

## Min SDK

We support a minimum SDK of 21. But the neumorphic components will be rendered appropriately only on devices running SDK version 28 or above.

## Contributing

Pull requests are welcome! We'd love help improving this library. Feel free to browse through open issues to look for things that need work. If you have a feature request or bug, please open a new issue so we can track it.

## Contributors

Synth would not have been possible if not for the contributions made by CRED's design and frontend teams. Specifically:
- Rishab Singh Bisht — [Twitter](https://twitter.com/rishabh1310) | [Github](https://github.com/rishabhsinghbisht) | [Linkedin](https://www.linkedin.com/in/rishabh-singh-bisht-b7550938/)
- Nikhil Panju — [Twitter](https://twitter.com/nikhilpanju) | [Github](https://github.com/nikhilpanju) | [Linkedin](https://www.linkedin.com/in/nikhilpanju/)
- Madhur Kapadia — [Twitter](https://twitter.com/madhurkapadia) | [Github](https://github.com/madhurkapadia) | [Linkedin](https://www.linkedin.com/in/madhurkapadia)
- Siddharth Kumar — [Twitter](https://twitter.com/itsiddharth_) | [Linkedin](https://www.linkedin.com/in/itssiddharth/)
- Hari Krishna

## License

```
Copyright 2020 Dreamplug Technologies Private Limited.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```