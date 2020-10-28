Inkscape Tips
========================================================================================

.. contents:: **Contents**

Berikut ini adalah *script* untuk mengubah jenis file dengan menggunakan
inkscape v0.92.5 di Terminal. 

Sebelum bisa menggunakan inkscape di Terminal. Inkscape harus dimasukkan ke Path:

::

	C:\Program Files\Inkscape
	
Ada dua cara untuk menjalankan *command*, yaitu via Terminal (Command Prompt) dan via Python.

via Terminal
----------------------------------------------------------------------------------------


Konversi SVG ke PDF
****************************************************************************************
::

	inkscape --file=tes.svg --export-pdf=tes.pdf

Konversi PDF ke SVG
****************************************************************************************

::

        inkscape --without-gui --file=tes.pdf --export-plain-svg=tes.svg
        

Konversi PDF to PNG
****************************************************************************************

::

	inkscape --file=tes.pdf -z --export-dpi=300 --export-area-drawing --export-png=tes.png

via Python
----------------------------------------------------------------------------------------

::

        # inkscapeConvert.py
        import os
        
        def svg2pdf(source):
            target = source.replace(".svg",".pdf")
            perintah = 'inkscape --file=' + source + ' --export-pdf=' + target
            os.system('cmd /k' + perintah + '')

        def pdf2svg(source):
            target = source.replace(".pdf",".svg")
            perintah = 'inkscape --without-gui --file=' + source + ' --export-plain-svg=' + target
            os.system('cmd /k' + perintah + '')
        
        def pdf2png(source):
            target = source.replace(".pdf",".png")
            perintah = 'inkscape --file=' + source + ' -z --export-dpi=300 --export-area-drawing --export-png=' + target
            os.system('cmd /k' + perintah + '')       

        # write the filename with extension here!
        source = 'impedanceDAB_cconv.pdf'
        
        # to use below script, just uncomment!
        # svg2pdf(source)
        # pdf2svg(source)
        # pdf2png(source)
        
Untuk menggunakan *script* di atas, ganti *source* dengan nama dari file yang ingin dikonversikan.

via Makefile
---------------------------------------------------------------------------------

Berikut ini contoh Makefile untuk mengkonversi dari pdf ke png.

::

        #convert pdf to png by Yohan
        #change-log
        #22-10-2020

        SRC:= $(wildcard *.pdf)
        OUT:= $(SRC:%.pdf=%.png)

        all: $(OUT)

        %.png: %.pdf
                inkscape --file=$< -z --export-dpi=300 --export-area-drawing --export-png=$@

