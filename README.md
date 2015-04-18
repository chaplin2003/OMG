# Overview
OMG is an open-source tool for the generation of chemical structures, implemented in the programming language Java(tm).

## Prerequisites
`OMG.jar` runs in the following OS:
- Ubuntu 32 bits
- Ubuntu 64 bits
- Mac OS X 64 bits

To build the `OMG.jar` you will need the following:
- [Ant 1.7](http://archive.apache.org/dist/ant/binaries/) or above
- JDK 6 or above
  * [OpenJDK 6](http://openjdk.java.net/install/) is **required** for Ubuntu users. Cause OMG builds [nauty](http://cs.anu.edu.au/~bdm/nauty/) via openjdk library. We can use `sudo apt-get install openjdk-6-jdk` to install openjdk.
  * For Mac users, there is no such limitation.
- cc/gcc installed. For Mac OS uses, clang is fine. For Ubuntu users, gcc will be ok.

## Build Steps
An ant build script is provided to generate the `OMG.jar`. Following ant tasks are available.
By default, we can just execute `ant` command under the project root directory to generate the `OMG.jar`.

1. Init
```bash
ant init
```
- This command will create temporary folders `dist` and `build`.
- `build` is the working directory while building process. `dist` is used for storing runnable `OMG.jar`.

2. Build
```bash
ant build
```
- We will build successfully if the `Prerequisites` are satisfied.
- This command will do the following:
	* Check the OS version and OS architecture.
	* Unpack `cdk` libraries and copy thirdparty libraries to the `build` folder.
	* Compile the nauty library according to the OS version and architecture.
	* Compile OMG java files.
- The mid-generated files during above steps are in `build` folder.

3. Dist
```bash
ant dist
```
- This command depends on the **build** task.
- A runnable `OMG.jar` is packed to `dist` folder. We can use it for verifying then.

4. Clean
```bash
ant clean
```
- This command will remove the `build` and `dist` folder.

5. Help
```bash
ant help
```
- This command will show the usage, including system info, java/ant info and and tasks info.

## Use OMG.tar
In order to use the `OMG.jar` in your program, you need to run the jar file via command line and provide some arguments.
```
-ec:  elemental composition of the molecules to be generated.
-o:   SDF file where to store the molecules.  
-fr:  SDF file containing prescribed one or multiple substructures. In the case
	    of multiple substructures, they have to be non-overlapping. 
```

Here there some examples of how to run OMG using the command line:
1. Generating molecules
	- Generate molecules for the elemental composition C6H6
	```bash
	java -jar OMG.jar -ec C6H6
	```
	- Generate molecules for the elemental composition C6H6 and store them in out_C6H6.sdf
	```bash
	java -jar OMG.jar -ec C6H6 -o out_C6H6.sdf
	```

2. Generating molecules with prescribed substructure(s)
	- Generate molecules for the elemental composition C2H5NO2 (glycine) using the prescribed substructure in fragment_CO2.sdf
	```bash
	java -jar OMG.jar -ec C2H5NO2 -fr fragment_CO2.sdf
	```

## Source Organization
This main sources are organized as follows:
```
`lib`: Thirdparty libraries, including licenses.
`src`: Source folder for OMG.
`testdata`: Some sample outputs via newly built OMG.jar.
`build.xml`: Ant script for building OMG.jar.
```
