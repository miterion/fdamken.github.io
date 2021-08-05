all: clean rasterize

clean:
	rm -f favicon.png favicon16x16.png favicon32x32.png apple_touch_icon.png safari_pinned_tab.png

rasterize:
	inkscape --without-gui logo.svg -w  48 -h  48 -o favicon.png
	inkscape --without-gui logo.svg -w  16 -h  16 -o favicon16x16.png
	inkscape --without-gui logo.svg -w  32 -h  32 -o favicon32x32.png
	inkscape --without-gui logo.svg -w 128 -h 128 -o apple_touch_icon.png
	inkscape --without-gui logo.svg -w 265 -h 256 -o safari_pinned_tab.png
