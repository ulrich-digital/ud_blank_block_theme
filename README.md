# Development Wordpress Block Theme

## Variable Fonts

### Create Variable WOFF2 Fonts

```
git clone --recursive https://github.com/google/woff2.git
cd woff2
```
In the woff2 directory:
```
make clean all
./woff2_compress path-to-font/variable-font.ttf
```

[https://henry.codes/writing/how-to-convert-variable-ttf-font-files-to-woff2/](https://henry.codes/writing/how-to-convert-variable-ttf-font-files-to-woff2/)

### Variable Fonts in theme.json

They are two issues in the Wordpress 6.0
1. a issue with font weight and styles
2. Multiple font-weights in one font-face declaration (chrome only)

Solution:
1. Rename the font (not font-file) in a unique String, which is certainly not installed on a system.
2. Add for every font-weight a fontFace declaration

This snippet is working 
```
{
	"version": 2,
	"customTemplates":[],
	"settings": {
		"typography": {
			"fontFamilies": [
				{
					"fontFamily": "\"Rubik UD\", sans-serif",
					"name": "Rubik UD",
					"slug": "rubik",
					"fontFace": [
						{
							"fontFamily": "Rubik UD",
							"fontWeight": "400",
							"fontStyle": "normal",
							"fontStretch": "normal",
							"src": [ "file:./fonts/Rubik-VariableFont_wght.woff2" ]
						},
						{
							"fontFamily": "Rubik UD",
							"fontWeight": "500",
							"fontStyle": "normal",
							"fontStretch": "normal",
							"src": [ "file:./fonts/Rubik-VariableFont_wght.woff2" ]
						},
						{
							"fontFamily": "Rubik UD",
							"fontWeight": "700",
							"fontStyle": "normal",
							"fontStretch": "normal",
							"src": [ "file:./fonts/Rubik-VariableFont_wght.woff2" ]
						},
						{
							"fontFamily": "Rubik UD",
							"fontWeight": "400",
							"fontStyle": "italic",
							"fontStretch": "normal",
							"src": [ "file:./fonts/Rubik-Italic-VariableFont_wght.woff2" ]
						},
						{
							"fontFamily": "Rubik UD",
							"fontWeight": "500",
							"fontStyle": "italic",
							"fontStretch": "normal",
							"src": [ "file:./fonts/Rubik-Italic-VariableFont_wght.woff2" ]
						},
						{
							"fontFamily": "Rubik UD",
							"fontWeight": "700",
							"fontStyle": "italic",
							"fontStretch": "normal",
							"src": [ "file:./fonts/Rubik-Italic-VariableFont_wght.woff2" ]
						}
					]
				}
			]
		}
	},
	
	"styles": {
		"elements": {
			"h2": {
				"typography": {
					"fontFamily": "Rubik UD",
					"fontWeight": "700"
				}
			}
		}
	}
}
```
## Navigation

Problem: Wenn eine Navigation ??ber das Template-File (i.e. header.html) eingef??gt werden soll, ist die Men??-ID unbekannt. Diese sollte vorhanden sein, damit die korrekten Men??-Eintr??ge ausgegeben werden k??nnen.

L??sungsansatz 1: Im Editor ein Navigations-Block hinzuf??gen, im Code-Editor den entsprechenden Code rauskopieren, Navigations-Block wieder l??schen.

L??sungsansatz 2: Bei kleinen Seiten (wenig Men??-Punkte) das Men?? gleich h??ndisch im header.html hinterlegen.
