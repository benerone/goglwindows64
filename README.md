# Using go-gl on windows 64 bits with golang 64 bits

## Step 1

Based on this [link](https://github.com/golang/go/wiki/InstallFromSource),
install [TDM-64-gcc](http://tdm-gcc.tdragon.net/download)

## Step 2

Based on this [link](https://bunkernetz.com/2013/09/01/building-go-glgl-on-windows/)
Download [glew source as zip archive](http://glew.sourceforge.net/)
Unzip

## Step 3

Based on this [link](https://stackoverflow.com/questions/6005076/building-glew-on-windows-with-mingw/6005262#6005262) and this [link](https://stackoverflow.com/questions/38673228/multiple-definition-of-dllmaincrtstartup12-while-building-glew-on-windows-wit)
Open shell (in my case, I use git shell), and execute commands:

> cd your unzipped directory

> gcc -DGLEW_NO_GLU -O2 -Wall -W -Iinclude  -DGLEW_BUILD -o src/glew.o -c src/glew.c

> gcc -nostdlib -shared -Wl,-soname,libglew32.dll -Wl,--out-implib,lib/libglew32.dll.a    -o lib/glew32.dll src/glew.o -L/mingw/lib -lglu32 -lopengl32 -lgdi32 -luser32 -lkernel32

## Step 4

Based on this [link](https://bunkernetz.com/2013/09/01/building-go-glgl-on-windows/)
from your unzipped directory
copy lib/libglew32.a in your install of TDM ->lib (in my case C:\TDM-GCC-64\lib)
copy include/GL  in your install of TDM -> include/GL (in my case C:\TDM-GCC-64\include\GL) 
the dll doesn't seem necessary.

## Step 5

then move to your go directory (GOPATH) and import go-gl

> go get -u github.com/go-gl/gl/v{3.2,3.3,4.1,4.2,4.3,4.4,4.5}-{core,compatibility}/gl
 
and exemple
 
> go get -u github.com/go-gl/example/gl41core-cube
 
build
 
> cd  src/github.com/go-gl/example/gl41core-cube
 
> go build
 
You have now gl41core-cube.exe
 
It works like a charm.
 
 