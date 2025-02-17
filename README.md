# photobooth

This is a fork of the photobooth fork (https://github.com/t0mmo/photobooth). I merged the fancytemplates branch, because I like it.
I miss a slideshow in case of inactivity. So I added this feature. I do some other changes, too.

Here is a list:
* add the slideshow 
* separate GPIO usage - different configuration of push buttons and lights
* GPIO push buttons changed - two buttons for trigger and a long hold press for exit function
* added some translations, but only in german 

To do's:
* improve the installation description for raspberry pi debian image bullseye, Qt installation changed a little
* GPIO buttons for the choice of printing 
* choice of two templates in the idle state
* preview in the start window

---

This is a fork from the original photobooth software (https://github.com/reuterbal/photobooth)

I use feature-branches for different things added. All get merged in the [mydev](https://github.com/t0mmo/photobooth/tree/mydev) branch. The master and development branches tend to reflect the original repository

## Additional Features
* [optimizedshotfilenames](https://github.com/t0mmo/photobooth/tree/optimizedshotfilenames) is an attempt to make the naming of shots and final pictures easier to understand. Eg the shots corresponding to photo001.jpg are now called photo001_shot1.jpg, photo001_shot2.jpg etc. See PR reuterbal/photobooth#164
* [fancytemplates](https://github.com/t0mmo/photobooth/tree/fancytemplates) allow for a much more flexible design of the templates.

### Fancy Templates

The templates are defined in XML. The XML file descibes size&color of the background. On top each XML tag adds an element on top of the others:
* `Image` can be PNG (incl transparency if required) or JPG etc and should be the same size like defined in the background. Can be used for a picture background or final overlay ontop of photos.
* `Photo` refers to a shot taken by the camera. Positioning, resizing, rotation are supported currently. Make sure shots are numbered correctly!

Currently, three examples are provided: 
* `standard_2x2.xml` mimics the current behaviour of composing 2x2 photos on a white back. <img alt="Example for standard 2x2 template" title="Standard 2x2 template" src="supplementals/templates/standard_2x2-result.jpg" width="280" />
* `example.xml` is a showcase for current capabilities (sorry for my limited design skills). Curious to see what others come up with! <img alt="Example for example template" title="Example template" src="supplementals/templates/example-result.jpg" width="280" />
* `photostrips.xml` is another showcase for what's possible <img alt="Example for photostrips template" title="Photostrips template" src="supplementals/templates/photostrips-result.jpg" width="280" />

To test & develop further templates the templating can be called directly from the CLI:
```
python -m photobooth.template.FancyTemplate -t .\supplementals\templates\example.xml
```
`-h` provides a short help

#### Further ideas for optimization 
(Please add/prioritize)
* [ ] caching of photo manipulations to increase speed
* [ ] resizing of image tag
* [ ] text tag to add text labels (almost same can be achieved by final overlay image including the text)

---

[![Buy me a coffee](https://www.buymeacoffee.com/assets/img/custom_images/black_img.png)](  )

A flexible Photobooth software.

It supports many different camera models, the appearance can be adapted to your likings, and it runs on many different hardware setups.

## Description
This is a Python application to build your own photobooth.

### Features
* Capture a single or multiple pictures and assemble them in an m-by-n grid layout
* Live preview during countdown
* Store assembled pictures (and optionally the individual shots)
* Printing of captured pictures (via Qt printing module or pycups)
* Highly customizable via settings menu inside the graphical user interface
* Custom background for assembled pictures
* Ability to skip single pictures in the m-by-n grid (e.g., to include a logo in the background image)
* Support for external buttons and lamps via GPIO interface
* Rudimentary WebDAV upload functionality (saves pictures to WebDAV storage) and mailer feature (mails pictures to a fixed email address)
* Theming support using [Qt stylesheets](https://doc.qt.io/qt-5/stylesheet-syntax.html)

### Screenshots
Screenshots produced using `CameraDummy` that produces unicolor images.

#### Theme _pastel_
<img alt="Idle screen" title="Idle screen" src="screenshots/pastel_1.png" width="280" /> <img alt="Greeter screen" title="Greeter screen" src="screenshots/pastel_2.png" width="280" /> <img alt="Countdown screen" title="Countdown screen" src="screenshots/pastel_3.png" width="280" /> <img alt="Postprocessing screen" title="Postprocessing screen" src="screenshots/pastel_4.png" width="280" /> <img alt="Settings screen" title="Settings screen" src="screenshots/pastel_settings.png" width="280" />

#### Theme _dark_
<img alt="Idle screen" title="Idle screen" src="screenshots/dark_1.png" width="280" /> <img alt="Greeter screen" title="Greeter screen" src="screenshots/dark_2.png" width="280" /> <img alt="Countdown screen" title="Countdown screen" src="screenshots/dark_3.png" width="280" /> <img alt="Postprocessing screen" title="Postprocessing screen" src="screenshots/dark_4.png" width="280" />

### Technical specifications
* Many camera models supported, thanks to interfaces to [gPhoto2](http://www.gphoto.org/), [OpenCV](https://opencv.org/),  [Raspberry Pi camera module](https://projects.raspberrypi.org/en/projects/getting-started-with-picamera)
* Tested on Standard x86 hardware and [Raspberry Pi](https://raspberrypi.org/) models 1B+, 2B, 3B, and 3B+
* Flexible, modular design: Easy to add features or customize the appearance
* Multi-threaded for responsive GUI and fast processing
* Based on [Python 3](https://www.python.org/), [Pillow](https://pillow.readthedocs.io), and [Qt5](https://www.qt.io/developers/)

### History
I started this project for my own wedding in 2015. 
See [Version 0.1](https://github.com/reuterbal/photobooth/tree/v0.1) for the original version.
Github user [hackerb9](https://github.com/hackerb9/photobooth) forked this version and added a print functionality.
However, I was not happy with the original software design and the limited options provided by the previously used [pygame](https://www.pygame.org) GUI library and thus abandoned the original version.
Since then it underwent a complete rewrite, with vastly improved performance and a much more modular and mature software design.

## Installation and usage

### Hardware requirements
* Some computer/SoC that is able to run Python 3.5+ as well as any of the supported camera libraries
* Camera supported by gPhoto 2 (see [compatibility list](http://gphoto.org/proj/libgphoto2/support.php)), OpenCV (e.g., most standard webcams), or a Raspberry Pi Camera Module.
* Optional: External buttons and lamps (in combination with gpiozero-compatible hardware)

### Installing and running the photobooth

See [installation instructions](INSTALL.md).

## Configuration and modifications
Default settings are stored in [`defaults.cfg`](photobooth/defaults.cfg) and can either be changed in the graphical user interface or by creating a file `photobooth.cfg` in the top folder and overwriting your settings there.

The software design is very modular.
Feel free to add new postprocessing components, a GUI based on some other library, etc.

## Feedback and bugs
I appreciate any feedback or bug reports.
Please submit them via the [Issue tracker](https://github.com/reuterbal/photobooth/issues/new?template=bug_report.md) and always include your `photobooth.log` file (is created automatically in the top folder) and a description of your hardware and software setup.

I am also happy to hear any success stories! Feel free to [submit them here](https://github.com/reuterbal/photobooth/issues/new?template=success-story.md).

If you find this application useful, please consider [buying me a coffee](https://www.buymeacoffee.com/reuterbal).


## License
I provide this code under AGPL v3. See [LICENSE](https://github.com/reuterbal/photobooth/blob/master/LICENSE.txt).
