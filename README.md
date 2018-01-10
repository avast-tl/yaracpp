# YARA C++ Wrapper

[![Travis CI build status](https://travis-ci.org/avast-tl/yaracpp.svg?branch=master)](https://travis-ci.org/avast-tl/yaracpp)

C++ wrapper for [YARA](https://github.com/VirusTotal/yara).

## Usage Example

```cpp
#include <iostream>
#include "yaracpp/yaracpp.h"

int main() {
    yaracpp::YaraDetector yara;
    yara.addRules(R"(
        rule example {
            strings:
                $s = "Hello"
            condition:
                $s
        })");
    yara.addRuleFile("/path/to/yara_file.yar");

    if (yara.analyze("/path/to/scanned/file")) {
        for (const auto& rule : yara.getDetectedRules()) {
            std::cout << rule.getName() << std::endl;
        }
    }
}
```

## Requirements

* A compiler supporting C++14
  * On Windows, only Microsoft Visual C++ is supported (version >= Visual Studio 2015).
* CMake (version >= 3.6)

## Build and Installation

* Clone the repository:
  * `git clone https://github.com/avast-tl/yaracpp.git`
* Linux:
  * `mkdir build && cd build`
  * `cmake -DCMAKE_BUILD_TYPE=<Debug|Release> ..`
  * `make`
* Windows:
  * Open MSBuild command prompt, or any terminal that is configured to run the `msbuild` command.
  * `mkdir build && cd build`
  * `cmake -G<generator> ..`
    * `-G<generator>` is `-G"Visual Studio 14 2015"` for 32-bit build using Visual Studio 2015, or `-G"Visual Studio 14 2015 Win64"` for 64-bit build using Visual Studio 2015. Of course, any later version of Visual Studio may be used.
  * `msbuild /m /p:Configuration=<Debug|Release> yaracpp.sln`
  * Alternatively, you can open `yaracpp.sln` generated by `cmake` in Visual Studio IDE.

## License

Copyright (c) 2017 Avast Software, licensed under the MIT license. See the `LICENSE` file for more details.

`yaracpp` uses third-party libraries or other resources listed, along with their licenses, in the `LICENSE-THIRD-PARTY` file.

## Contributing

See [RetDec contribution guidelines](https://github.com/avast-tl/retdec/wiki/Contribution-Guidelines).
