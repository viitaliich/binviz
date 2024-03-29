# Files Binary Visualization

This implementation of Files Binary Visualisation is inspired by:
- Christopher Domas talk: https://www.youtube.com/watch?v=4bM3Gut1hIk
- Tsoding Daily video - Reverse Engineering Data Files: https://youtu.be/AUWxl0WdiNI?si=7xVg1Mnc2CtXbJnw

**stb** library is used in code: https://github.com/nothings/stb

## Explanation

The main idea of this project is to take a computationally difficult task, such as big file reverse engineering, and translate it to a problem our brains do naturally.

This became possible, since even in 'unstructured' data there is a structure.
Sequential bytes have an implicit relationship.

To see this hidden structure, all we need to do is to take sequential bytes of the file and translate them to coordinates on a 2D plane.

![IMG_20240120_190716_556](https://github.com/viitaliich/binviz/assets/47535508/f37efbc8-2d88-4850-8b4a-8f192ac1e08c)

Different types of files have different patterns on a result image. 

Also each part of the pattern is responsible for specific type of data.
On the image below pattern for ASCII text is presented:

![IMG_20240120_190638_718](https://github.com/viitaliich/binviz/assets/47535508/45bf8ff8-7d81-4eed-946d-51b94dee066f)

Using these patterns, we can detect file type knowing nothing about it 🙂

## Examples

### ASCII english, cyrillic, .docx, .pdf respectively.

![VIZ text txt](https://github.com/viitaliich/binviz/assets/47535508/7c3d2a44-6251-4651-882f-a204e9656088)
![VIZ CyrillicFile txt](https://github.com/viitaliich/binviz/assets/47535508/15ab9127-ca40-4da5-9e52-dbd0d68681db)
![VIZ DOCXfile docx](https://github.com/viitaliich/binviz/assets/47535508/a718b1c6-85b2-4bcc-b044-a6e319d9e417)
![VIZ PDFfile pdf](https://github.com/viitaliich/binviz/assets/47535508/41f06c54-7ba9-43e2-a9fd-4e9f62e23bba)

### Image .raw, .png .jpg respectively.

![VIZ image png raw](https://github.com/viitaliich/binviz/assets/47535508/7d1c5ce9-39a9-4b72-b1dd-5dc8680bd3e5)
![VIZ image png](https://github.com/viitaliich/binviz/assets/47535508/7b0032d0-84c9-4e6b-acfd-c85f12a3be78)
![VIZ JPGimage jpg](https://github.com/viitaliich/binviz/assets/47535508/cb044c03-0da4-4b15-81ac-b833c9532b67)

### Audio .wav, .mp3 respectively.

![VIZ wav_audio wav](https://github.com/viitaliich/binviz/assets/47535508/60abb93a-1bd7-4c2e-912b-7637fda58b67)
![VIZ MP3audio_4 mp3](https://github.com/viitaliich/binviz/assets/47535508/af95621e-0edd-4455-bc1f-f7cd43d1683b)

### Executable x86_64, .zip respectively.

![VIZ EXEexe exe](https://github.com/viitaliich/binviz/assets/47535508/a5a11a71-ae9a-4595-a8d7-b552a29e0bb1)
![VIZ ZIPfile zip](https://github.com/viitaliich/binviz/assets/47535508/461baa3c-c58b-444d-93a8-feb900ba5845)

As can bee seen, some files are compressed, that has impact on result image.

## How to start

1. Modify **premake5.lua** file to set proper pathes to your files.
   ```
   filter "configurations:Debug"
	defines { "DEBUG" }
	runtime "Debug"
	symbols "on"
	debugargs { 
		"C:\\dev\\Binviz\\data\\text.txt",
		"C:\\dev\\Binviz\\data\\image.png",
		"C:\\dev\\Binviz\\data\\image.png.raw",
		"C:\\dev\\Binviz\\data\\wav_audio.wav"
	}
   ```

2. Run **GenerateProjects.bat** file to generate Visual Studio solution file.

## What next?

- [ ] Larger result images
- [ ] Raw video support
- [ ] Another type of coordinate system
- [ ] 3D visualisation
- [ ] Proper renderer
- [ ] Premake for Mac, Linux
- [ ] Neural network 🙂
