androidbinary
=====

[![Build Status](https://travis-ci.org/tap4fun/androidbinary.svg?branch=master)](https://travis-ci.org/tap4fun/androidbinary)
[![GoDoc](https://godoc.org/github.com/tap4fun/androidbinary?status.svg)](https://godoc.org/github.com/tap4fun/androidbinary)

Android binary file parser

## High Level API

### Parse APK files

``` go
package main

import (
	"github.com/tap4fun/androidbinary/apk"
)

func main() {
	pkg, _ := apk.OpenFile("your-android-app.apk")
	defer pkg.Close()

	icon, _ := pkg.Icon(nil) // returns the icon of APK as image.Image
	pkgName := pkg.PackageName() // returns the pakcage name
}
```

## Low Lebel API

### Parse XML binary

``` go
package main

import (
	"encoding/xml"

	"github.com/tap4fun/androidbinary"
	"github.com/tap4fun/androidbinary/apk"
)

func main() {
	f, _ := os.Open("AndroidManifest.xml")
	xml, _ := androidbinary.NewXMLFile(f)
	reader := xml.Reader()

	// read XML from reader
	var manifest apk.Manifest
	data, _ := ioutil.ReadAll(reader)
	xml.Unmarshal(data, &manifest)
}
```

### Parse Resource files

``` go
package main

import (
	"fmt"
	"github.com/tap4fun/androidbinary"
)

func main() {
	f, _ := os.Open("resources.arsc")
	rsc, _ := androidbinary.NewTableFile(f)
	resorce, _ := rsc.GetResource(androidbinary.ResID(0xCAFEBABE), nil)
	fmt.Println(resource)
}
```

## License

This software is released under the MIT License, see LICENSE.
