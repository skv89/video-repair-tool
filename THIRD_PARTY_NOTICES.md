# Video Repair Tool — Third-Party Notices

Video Repair Tool 1.9.1 includes TkinterDnD2 0.6.2 and its TkDND native extension
for Windows Explorer drag-and-drop. The executable is created with PyInstaller
and includes the Python runtime and Tcl/Tk components required to start the GUI.

FFmpeg, FFprobe, VapourSynth, Python embedded distributions, VSJetpack, and
optional GPU packages are not embedded media dependencies in the executable.
With explicit user consent, this app's local dependency installer downloads
FFmpeg/FFprobe to a separate managed runtime beside the application without
modifying system PATH, registry, or existing installations. Other optional
packages listed below may be present in a shared runtime installed by another
video tool; this repair app does not require them.

## Optional app-local dependencies

- Gyan FFmpeg full build: GPLv3; individual FFmpeg components retain their
  respective upstream licenses.
- VapourSynth portable release: LGPL-2.1-or-later.
- Python embedded distribution: Python Software Foundation License.
- VSJetpack and Python support packages: MIT, with native plugins retaining
  their respective upstream licenses.
- Optional NVIDIA/CUDA components retain NVIDIA's proprietary licenses.

## PyInstaller

PyInstaller is distributed under GPL-2.0-or-later with a special exception that
permits distributing executables produced by PyInstaller under terms of the
application author's choice. See the PyInstaller project for the complete
license and bootloader exception.

## TkinterDnD2

MIT License

Copyright (c) 2020 Philippe Gagné

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## TkDND

This software is copyrighted by Georgios Petasis, Athens, Greece. Mac portions
are copyright 2009–2014 Kevin Walzer/WordTech Communications LLC.

The authors grant permission to use, copy, modify, distribute, and license the
software and its documentation for any purpose, provided existing copyright
notices are retained and this notice is included in distributions. The software
is provided "AS IS" without warranty; the authors and distributors disclaim
liability for direct, indirect, special, incidental, or consequential damages.
