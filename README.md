# EKM: Eno Keyboard Mapping
If you pressed the "a" key, different keyboard actually may send different signal(scancode), but after this signal processed by the operating system(keyboard driver), it will generate the same keycode 90, which stands for "a".

We can hardly change the signal, but not hard to change the keycode, which makes remapping the keyboard possible.

While other keyboard layout simply remap character keys, EKM take a step further by remapping almost every single key, provides additional key combinations and even simultaneously pressed keys.

Since the layout part is hard to learn/memorize thus might not worth the payoff, EKM also provides a starter mapping that doesn't change the layout.

- [Background Knowledge](#sec-1)
- [EKM-starter](#sec-2)
- [Karabiner / How to use](#sec-3)
- [EKM](#sec-4)
- [Customization](#sec-5)
- [Reference](#sec-6)

# <a id="sec-1"></a> Background Knowledge
## virtual modifier keys and overlay

When you "pressed" a key, there're actually 2 signals been sent, one for key-down, one for key-up, for normal keys, the key-down signal will Immediately map to the keycode, for modifier keys, the OS will wait until the key-up signal, if there is a normal key-down signal, then send a key combination like Command+A.

This means we can not only make virtual modifier keys, but also "overlay" a normal key to a modifier key and vice versa(e.g. Space key can also be Command key).

The downside is if you press two keys too fast, it will send a key combination instead of two normal keys, so it's better not overlay any character key.

EKM have used this to map number keys and movement keys.

## simultaneous key press

If you press "s" and "d" at the same time, you'll enter either "sd" or "ds", this is useless, but how about mapping it to "Cmd+c", or "!", or "Up"?

Today's computer is fast enough to differentiate signals in milliseconds, so it's possible to tell computer to treat two consecutive key-down signals in 30ms as a "simultaneous key press".

EKM have used this to map symbol keys and key combinations.

# <a id="sec-2"></a> EKM-starter

EKM-starter is created for people who don't want to change the original keyboard, thus only adding extra figure on it.

## modifier overlay
![image](https://cloud.githubusercontent.com/assets/13136462/8763504/daa227c0-2dd1-11e5-9013-b4022301d198.png)

EKM-starter overlaid forward Delete to left Control, Delete to left Shift, Enter to left Command, and Esc to right command.

## modifier keys pressed
EKM created a virtual modifier key randomly named "zZ", EKM-starter overlays it to Space, when it is pressed:

![image](https://cloud.githubusercontent.com/assets/13136462/8762953/6930d616-2dba-11e5-812f-002cb9dbcfb3.png)

EKM also utilize the FN modifier key by overlay it to down key,when it is pressed:

(press it using right palm, for thin keyboard, stick something 0.8cm high on it)

![image](https://cloud.githubusercontent.com/assets/13136462/8763022/b9a502b8-2dbd-11e5-96c8-08eba6c9a49b.png)

(also overlaid ";" key to "command+fn", so ";+a" becomes "command+1")

## simultaneously pressed keys
EKM maps the simultaneously pressed keys "as" to "Cmd+x", "sd" to "Cmd+c", "df" to "Cmd+v", and left control + right hand character keys to open application:

![image](https://cloud.githubusercontent.com/assets/13136462/8763087/8b8b0b2c-2dc0-11e5-98fb-4b8c169762f9.png)

([Change them](https://github.com/enoson/EKM/blob/master/starter.xml#L66) to your most used [applications](https://pqrs.org/osx/karabiner/xml.html.en#vkopenurldef))

EKM-starter maps left command + character keys to symbols:

![image](https://cloud.githubusercontent.com/assets/13136462/8763086/7e417b90-2dc0-11e5-8307-365180e0fb5b.png)

Since other application can't recognize simultaneous keys, EKM maps 500+ simultaneous keys to key combinations that's unlikely used(e.g. ⌘⌥⇧+a or ⌘+F1), see the full list in [simul2combo-map.xml](https://github.com/enoson/EKM/blob/master/simul2combo-map.xml), or use some keystroke visualizer like [KeyCastr](https://github.com/keycastr/keycastr).
(c:control, h:command, m:option, s:shift)

# <a id="sec-3"></a> Karabiner / How to use
All of the above mapping will be tedious to achieve without [Karabiner](https://pqrs.org/osx/karabiner/) - by far the best keyboard mapping tool on Mac, similar softwares on Windows or Linux have less figures and even buggy.

This repo is just the configuration files for Karabiner, install it if you haven't, then either clone this repo to Karabiner's config directory by:
`cd ~/Library/Application\ Support/Karabiner&&find * -print0  | xargs -0  rm -rv&&git clone https://github.com/enoson/EKM.git .`

or download (, extract) and put these files to [the Karabiner directory](https://pqrs.org/osx/karabiner/document.html.en#privatexml):`~/Library/Application Support/Karabiner`

Reload:

![image](https://cloud.githubusercontent.com/assets/13136462/8876588/36a3ecfe-3253-11e5-8ebf-3e4e1fd973ee.png)

Enable the mappings: (starter)

![image](https://cloud.githubusercontent.com/assets/13136462/8763249/8b5262e4-2dc6-11e5-9ebe-b1df3f0ab53e.png)

[Create a profile](https://pqrs.org/osx/karabiner/document.html.en#profiles) and then check the mappings you need so that you can switch between different configurations:

![image](https://cloud.githubusercontent.com/assets/13136462/8763279/03af6674-2dc7-11e5-888a-e4b19348fc7f.png)

Lower the threshold depending on how fast you type:

![image](https://cloud.githubusercontent.com/assets/13136462/8763288/59c4489a-2dc7-11e5-81ef-adb18fc8faa2.png)

# <a id="sec-4"></a> EKM
I, like many other people, have used the QWERTY keyboard layout for many years, not aware of how slow it is, until one day I tried the Dvorak  layout:

![image](https://cloud.githubusercontent.com/assets/13136462/8763300/be642fe0-2dc7-11e5-87d2-dd44d92024b3.png)

Immediately I realized the slowness of QWERTY.

The reason is twofold, the first is distance, while Dvorak puts the most frequent Vowels & Consonants on the home row, QWERTY only puts "AS". The second is fluency, while Dvorak puts "',.;QJ" around "AOE" to avoid typing two consecutive letter with one finger, QWERTY basically has done nothing about it.

However, Dvorak is still far from perfect, e.g. "I","F" is hard to press. I know perfect is impossible, but I want to be as near as possible, so I started to roll my own layout. Theoretically, a perfect layout would arrange the most typed key to the fastest position, one by one until the least typed key, while keeping all the possible consecutive keys that are into different finger.
(e.g. there are few words contains "je" or "ej", but are many words contains "de" or "ed".)

Since there are 5 vowels and 10 keys around them, these two requirements are impossible to meet at the same time, for a long time I couldn't even found an acceptable arrangement, until I made a radical switch by map space to "e" and map "i","u" to same finger:

![image](https://cloud.githubusercontent.com/assets/13136462/8763522/1d11a396-2dd3-11e5-8a14-e4d87cf38a5d.png)

Put your right forefinger on the original "k" key instead of "j", so your right thumb can put on the original right command by default.

Install [Seil](https://pqrs.org/osx/karabiner/seil.html.en) to map `capslock` to `Forward Delete`(117):

![image](https://cloud.githubusercontent.com/assets/13136462/8763333/5896e7e6-2dc9-11e5-8538-81939e532635.png)

EKM overlays the virtual modifier key "zZ" to the original "k" key, and when it is pressed:

![image](https://cloud.githubusercontent.com/assets/13136462/8763480/8f48b164-2dd0-11e5-9dbe-f263b68b97db.png)

EKM maps simultaneously pressed right command + character keys to symbols:

![image](https://cloud.githubusercontent.com/assets/13136462/8763493/dc247996-2dd0-11e5-8528-75d928973292.png)

# <a id="sec-5"></a> Customization
One size does not fit all, so you can and should modify these config files to suit your own need or "include" new config file at the beginning.(if a mapping is defined, subsequent mapping will not take effect)

## ~/Library/Application Support/Karabiner/privite.xml
This is the entry file that Karabiner loads by default, it's possible to put all the configs here, but then if you have one error, all your config will break, so EKM divides it to several files, then includes them here in a specific order:
```
<include path="abbreviation.xml"/>
<include path="personal.xml"/>
<include path="non-apple-mod.xml"/>
<include path="starter.xml"/>
<include path="combination.xml"/>
<include path="simultaneous.xml"/>
<include path="simul2combo-map.xml"/>
<include path="starter-layout.xml"/>
<include path="layout-top.xml"/>
<include path="layout-middle.xml"/>
<include path="layout-bottom.xml"/>
```

###### abbreviation.xml
The original Karabiner config format is verbose, so I defined [abbreviations](https://pqrs.org/osx/karabiner/xml.html.en#replacementdef) for most keys, which makes customization easier.

###### personal.xml
Default file for personal config, e.g. I use a track-point keyboard that has PrintScreen key on the original right windows key, so I need to remap it but others probably don't need.

###### non-apple-mod.xml
Override some EKM mappings for non Apple keyboard that has windows key instead of command..

###### starter.xml
Override some EKM mappings for EKM-starter.

###### combination.xml
Default EKM key combination mappings.

###### simultaneous.xml
Default EKM simultaneous key mappings.

###### simul2combo-map.xml
500+ simultaneous key to key combination mappings.

###### starter-layout.xml
Override some EKM layout mappings for EKM-starter.

###### layout-top.xml, layout-middle.xml, layout-bottom.xml
Default EKM layout, remember to put layout remap at last so it won't mess up other config.

## enable EKM

![image](https://cloud.githubusercontent.com/assets/13136462/8763348/f68c88ac-2dc9-11e5-819e-7bf199d2dbe0.png)

# <a id="sec-6"></a> Reference
- [usage manual](https://pqrs.org/osx/karabiner/document.html.en)
- [config formats document](https://pqrs.org/osx/karabiner/xml.html.en)
- [single keys](https://github.com/tekezo/Karabiner/blob/master/src/bridge/generator/keycode/data/KeyCode.data)
- [modifier keys](https://github.com/tekezo/Karabiner/blob/master/src/bridge/generator/keycode/data/ModifierFlag.data)
- [sample configs](https://github.com/tekezo/Karabiner/blob/master/src/core/server/Resources/include/checkbox/samples.xml)
