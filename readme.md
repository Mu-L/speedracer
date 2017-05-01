<p align="center">
  <img alt="Speed Racer" src="https://raw.githubusercontent.com/ngryman/artworks/master/speedracer/heading/speedracer@2x.png">
</p>

<p align="center">
  Collect performance metrics for your library/application.
</p>

<p align="center">
  <a href="//travis-ci.org/ngryman/speedracer">
    <img alt="Build Status" src="https://img.shields.io/travis/ngryman/speedracer.svg">
  </a>
</p>

---

## Installation

```sh
npm install -g speedracer
```

**Speed Racer** needs Chrome to profile your files.
Preferably, if you have Chrome Canary installed it will run it headless.


## Usage

```sh
$ speedracer -h

  🚗  Speed Racer v0.1.0

  speedracer files [options]

  Options:

    -h, --help            Usage information  false
    -t, --traces          Save traces        false
    -r, --reports         Save reports       false
    -o dir, --output=dir  Output directory   ./.speedracer

  Examples:

  – Race files in perf directory:

    $ speedracer

  – Race files matching perf/**/*.js glob:

    $ speedracer perf/**/*.js

  – Save traces and reports:

    $ speedracer --reports --traces --output=./speedracer
```

## Reports

Reports are `json` files that contain a performance summary of your run. They give you insight of what is taking time and why. 

They can be useful to track performance regression. You can save those reports and compare them with new ones before commiting changes. You will then know if the new changes affected performance in a wrong way.

Here is the format:
```json
{
  "name": "render-loop.js",
  "profiling": {
    "categories": {
      "scripting": 59.44300004839897,
      "rendering": 51.38299997150898,
      "painting": 41.349999979138374,
      "loading": 4.573000013828278
    },
    "events": {
      "Animation Frame Fired": 39.61099997162819,
      "Composite Layers": 32.80699998140335,
      "Update Layer Tree": 27.93999993801117,
      "Recalculate Style": 23.179000034928322,
      "JS Frame": 15.728000089526176,
      "Paint": 8.542999997735023,
      "Parse HTML": 4.573000013828278,
      "Evaluate Script": 3.408999979496002,
      "Compile Script": 0.6950000077486038,
      "Layout": 0.2639999985694885
    },
    "functions": {
      "FireAnimationFrame": 39.61099997162819,
      "CompositeLayers": 32.80699998140335,
      "UpdateLayerTree": 27.93999993801117,
      "UpdateLayoutTree": 23.179000034928322,
      "f:requestAnimationFrame@": 8.663000077009201,
      "Paint": 8.542999997735023,
      "f:render@25": 6.45100000500679,
      "ParseHTML": 4.573000013828278,
      "EvaluateScript": 3.408999979496002,
      "v8.compile": 0.6950000077486038,
      "f:@24": 0.3190000057220459,
      "f:@25": 0.29500000178813934,
      "Layout": 0.2639999985694885
    }
  },
  "firstPaint": 0.028327,
  "fps": {
    "mean": 60.2,
    "variance": 1.6,
    "sd": 1.26,
    "lo": 55.66,
    "hi": 65.97
  }
}
```

## Traces

Speed Racer can save traces of your runs. Traces contains events emitted by Chrome when your script is executed. Those events gives a bunch of informations about the overall performance of your script. Here is the detail [format](https://docs.google.com/document/d/1CvAClvFfyA5R-PhYUmn5OOQtYMH4h6I0nSsKchNAySU/preview#heading=h.uxpopqvbjezh).

You can use those traces to analyze them the way you want or simply load them in the Timeline/Performance tab of Chrome.
Traces can be big, so they are saved `gzip`.

### Load in Devtools

First you need to locate and decompress your trace.

```sh
$ cd .speedracer
$ ls
high-cup.trace.gz
$ gunzip high-cup.trace
```

Then you load it in Chrome Devtools and enjoy :tada:!

If you are interesHere is a detail of the raw format: https://docs.google.com/document/d/1CvAClvFfyA5R-PhYUmn5OOQtYMH4h6I0nSsKchNAySU/preview#heading=h.uxpopqvbjezh,
