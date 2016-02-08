# LeMonADE-Viewer
The abbreviation LeMonADE stands for 
"**L**attice-based **e**xtensible **Mon**te-Carlo **A**lgorithm and **D**evelopment **E**nvironment"
and "Viewer" refers to the visualization module.

The aim of the application LeMonADE-Viewer is to provide a simplistic visualization tool
for rendering the bond-fluctuation-model [1] [BFM1] [2] [BFM2] data generated by the LeMonADE-project [3] [LeMonADE-project].

For further details of LeMonADE-project see: [LeMonADE-project]


[BFM1]: http://dx.doi.org/10.1021/ma00187a030  "I. Carmesin, K. Kremer; Macromolecules 21, 2819-2823 (1988)"
 
[BFM2]: http://dx.doi.org/10.1063/1.459901 "H. P. Deutsch, K. Binder; J. Chem. Phys. 94, 2294-2304 (1990)"

[LeMonADE-project]: https://github.com/LeMonADE-project/

## Installation

* Clone the LeMonADE library `git clone https://github.com/LeMonADE-project/LeMonADE.git`
* Install the LeMonADE library - see [LeMonADE-project] 
* Clone the LeMonADE-Viewer application `git clone https://github.com/LeMonADE-project/LeMonADE-Viewer.git`
* Install cmake (minimum version 2.6.2)
* Install FLTK and OpenGL (devel)
* Install POV-Ray for high resolution rendering 
* Just do for standard compilation (program):

````sh
    # generates the application in build-directory
    ./configure -DLEMONADE_DIR=/path/to/LeMonADE/
    make
````

 or
 
````sh
    # generates the application in build-directory
    mkdir build
    cd build
    cmake -DLEMONADE_DIR=/path/to/LeMonADE/ ..
    make
````

## Getting Started

````sh
    # rendering a test-bfm-file
    cd build/
    ./LeMonADE-Viewer ../test.bfm
````
## Troubleshooting

* Problem: Build fails with linker error:

````sh
	/usr/bin/ld: cannot find -lLeMonADE
````
  Solution: 
  LeMonADE is not properly installed, or the option -DLEMONADE_DIR was set incorrectly.
  (a) Install the LeMonADE library to a default system path
  (b) Install the LeMonADE library to a custom path and hand this path 
      to the configure script, or cmake, depending on your choice of build method

````sh
	./configure -DLEMONADE_DIR=/custom/install/path/to/LeMonADE
	make
````
  For installation instructions to the LeMonADE library see https://github.com/LeMonADE-project/LeMonADE


* Problem: On Ubuntu (tested with Ubuntu 14.04), build fails with linker error:

````sh
	/usr/bin/ld: undefined reference to symbol 'dlsym@@GLIBC_2.2.5'
````
  Solution: Add the following to src/LeMonADE-Viewer/CMakeLists.txt:
  Original line:
````sh
	target_link_libraries(${APPLICATION_NAME} ${OPENGL_LIBRARIES} ${FLTK_LIBRARIES} Camera LineParser LeMonADE)
````

  Changed line:
````sh
	target_link_libraries(${APPLICATION_NAME} ${OPENGL_LIBRARIES} ${FLTK_LIBRARIES} Camera LineParser LeMonADE dl)
````


  Then, re-run the build instructions.
  
* Problem: On Ubuntu (tested with Ubuntu 14.04), build fails with linker error:

````sh
	/usr/bin/ld: cannot find -lpng
````
  Solution: Install development package for libpng12
  
````sh
	sudo apt-get install libpng12-dev
````  

* Problem: On Ubuntu (tested with Ubuntu 14.04), build fails with linker error:

````sh
	/usr/bin/ld: cannot find -lz
````
  Solution: Install development package for zlib1g
  
````sh
	sudo apt-get install zlib1g-dev
````  

* Problem: On Ubuntu (tested with Ubuntu 14.04), build fails with linker error:

````sh
	/usr/bin/ld: cannot find -lSOME_LIBRARY_NAME
````
  where SOME_LIBRARY_NAME one of (jpeg,Xft,fontconfig,Xinerama)
  
  Solution: Install development package for libSOME_LIBRARY_NAME
  
````sh
	sudo apt-get install libSOME_LIBRARY_NAME-dev
````


## License

See the LICENSE in the root directory.
