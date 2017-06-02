# ue4_doxygen_source_filter

This is a small [Python 3](https://www.python.org/) script intended to allow the [Doxygen](http://www.stack.nl/~dimitri/doxygen/) documentation tool to be run on C++ code which is using [Unreal Engine 4](https://www.unrealengine.com/what-is-unreal-engine-4).

This is done by filtering C++ code to look for things which look like UE4 macros and commenting them out, and won't cause problems with your main build as the commented-out version is only passed to Doxygen.  It also won't affect the line numbers so anything Doxygen needs those for it fine.

This does have limitations:
* It will miss the side-effects of the macros such as GENERATED_BODY making variables Public.
* It won't work if you have /\* ... \*/ comments in your UE4 macros, this is a Todo and so may be fixed when I get time.
* It can only handle 25 levels of balanced nested parentheses in your source code.  It doesn't look at whether a parentheses is inside a string either so be careful with that.
* It assumes each macro will start on line by itself with optional spaces in front of it- this is to stop it doing strange things with any strings which may look like macros.
* It only catches UFUNCTION, UCLASS, UPROPERTY and UENUM- although adding more is simple enough- just add them as another item in the regular expression.
* &hellip;I've not had the time to run this over the UE4 codebase itself to see how it does.

So, it's not perfect, but it means I can use Doxygen for my own code and this makes me unreasonably happy.

## Usage
To use this you'll need Doxygen and Python3 installed on your machine.  Put this script somewhere sensible and inside your doxygen.conf edit the *INPUT_FILTER* setting to point to the path- now Doxygen should call this when you build your documentation and the macros should no longer cause problems.

## License
[MIT License](https://en.wikipedia.org/wiki/MIT_License)

Copyright (c) 2017 Paul Golds

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
