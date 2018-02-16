# vscode-glsl-canvas

The extension opens a live WebGL preview of GLSL shaders within VSCode by providing a ```Show glslCanvas``` command.

It use [glslCanvas](https://github.com/patriciogonzalezvivo/glslCanvas) a javaScript library from [Book of Shaders](http://thebookofshaders.com) and [glslEditor](http://editor.thebookofshaders.com) made by [Patricio Gonzalez Vivo](http://patriciogonzalezvivo.com).

*Run the command to display a fullscreen preview of your fragment shader.*

![example](https://rawgit.com/actarian/vscode-glsl-canvas/master/src/preview-half.gif)

-----------

## Uniforms

The uniforms provided are ```u_resolution```, ```u_time```, ```u_mouse```. You can define the texture channels (```u_texture_0```, ```u_texture_1```, ...) by modifying the workspace's ```settings.json``` file. 
```
{
    "glsl-canvas.textures": {
        "0": "./texture.png",
        "1": "https://rawgit.com/actarian/plausible-brdf-shader/master/textures/noise/cloud-1.png",
        "2": "https://rawgit.com/actarian/plausible-brdf-shader/master/textures/noise/cloud-2.jpg",        
    }
}
```

## Custom Uniforms

You can also define custom uniforms by modifying the workspace's ```settings.json``` file. 

```
{
    "glsl-canvas.uniforms": {
        "u_strength": 1.0
    }
}
```

Types supported are ```float```,  ```vec2```,  ```vec3``` and ```vec4```. Vectors structures are converted from arrays of floats. Range values goes from ```0.0``` to ```1.0```.

| Type                    | Property                         |
|-------------------------|----------------------------------|
| `float`                 | "u_float":  1.0,                 |
| `vec2`                  | "u_vec2":  [1.0, 1.0],           |
| `vec3`                  | "u_vec3":  [1.0, 1.0, 1.0],      |
| `vec4`                  | "u_vec4":  [1.0, 1.0, 1.0, 1.0], |

## Uniforms Gui

By clicking the option button you can view and modify at runtime uniforms via the [dat.gui](https://github.com/dataarts/dat.gui) interface.

![example](https://rawgit.com/actarian/vscode-glsl-canvas/master/src/preview-gui.gif)

## Fragment shader

An example of fragment shader. You can copy paste this code in an empty `.glsl` file:

```glsl
precision mediump float;

uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_time;

void main() {
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    st.x *= u_resolution.x/u_resolution.y;

    vec3 color = vec3(0.);
    color = vec3(st.x,st.y,abs(sin(u_time)));

    gl_FragColor = vec4(color,1.0);
}
```

## Features

* Integrated support of error handling with lines hilight.
* Play / pause functionality.
* Recording and exporting to ```.webm``` video.
* Activable [stats.js](https://github.com/mrdoob/stats.js/) performance monitor.
* Custom uniforms.
* Activable gui for changing custom uniforms at runtime.
* Glsl Snippets.

## Glsl Snippets

| Snippet                      | Purpose                         |
|------------------------------|---------------------------------|
| `glsl.main.new`              | Main function, uniforms & utils |
| `glsl.math.2d.transform`     | Math 2D Transformations         |
| `glsl.math.3d.transform`     | Math 3D Transformations         |
| `glsl.shapes.2d.box`         | Shape 2D box                    |
| `glsl.shapes.2d.circle`      | Shape 2D circle                 |
| `glsl.shapes.2d.poligon`     | Shape 2D polygon                |

## Requirements

* A graphics card supporting WebGL.

-----------

## Todo

* Improved snippets library.
* Glsl code formatting.

## Contributing

[Github Project Page](https://github.com/actarian/vscode-glsl-canvas)  
[Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=circledev.glsl-canvas)

*Thank you so much for taking the time to provide feedback and review. This feedback is appreciated and very helpful.*

## Release Notes

### 0.1.5

* Gui for changing custom uniforms at runtime.
* Fix dependancy from other extension.

### 0.1.3

* Play / pause functionality.
* Record button that exports to ```.webm``` video.
* Activable performance monitor.
* Better handling of active ```.glsl``` editor.
* Improved inline error message.
* Fix resizing issue.
* Minor snippets functionality.

### 0.1.1

* Initial release of glsl-canvas for vscode.
