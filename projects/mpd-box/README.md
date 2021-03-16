# MPD BOX on Pimoroni's Phat Beat / pirate radio
- Use [Python Music Player Daemon](https://www.musicpd.org/) as a service to play both local files and playlists (including radio urls) on the phat beat.
- Use [beets](http://beets.io/) (optionnaly ?) to organize / import the local music library
- Use [MPD client lib](https://www.musicpd.org/libs/python-musicpd/) in a python script running as a service. It will act as a MPD client to control the local MPD server service, through the phat beat buttons
- Others clients should be able to control played music through the local network. (Many android clients are available)

## Controls
Use button holding (next / prev) to cycle through playlists.

## LED
Replace green only pivumeter by a rainbow one. Integrated within the _client_ service or decoupled ?

Something along this :

```python
def set_volume(self, level=3):
    if level >= 0 and level <= 8:
        self.volume = level
        self.player.set_volume(self.volume*12) # 0-96
        self.show_volume(level)

def volume_up(self, pin):
    self.set_volume(self.volume + 1)

def volume_down(self, pin):
    self.set_volume(self.volume - 1)

def show_volume(self, level, saturation=1.0, value=0.2):
    phatbeat.clear()
    for i in range(0,8):
        # definition de la teinte en fonction de la "hauteur" du pixel
        # pour un effet "arc en ciel"
        # on divise 360° par 8 "crans" (=45°)
        # et on decale arbitrairement de 45° pour ne pas débuter sur rouge
        hue = 315 - 45*i # definition de la teinte (8 crans = 45°)
        if level > i:
            r, g, b = [int(x * 255) for x in colorsys.hsv_to_rgb(hue / 360.0, saturation, value)]
            phatbeat.set_pixel(7-i, r, g, b, 0.1, channel=0)
            phatbeat.set_pixel(7-i, r, g, b, 0.2, channel=1)
    phatbeat.show()

```
