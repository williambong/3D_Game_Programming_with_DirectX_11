## How to Read `float` Elements of `XMMATRIX` - () operator not working

Individual element access for `XMVECTOR` and `XMMATRIX` is very inefficient due to the underlying SIMD instruction set, so the DirectXMath library doesn't support it through member methods.

If you are going to access most or all of the individual elements of an `XMMATRIX`, the best solution is to dump it to an `XMFLOAT4X4` as shown in lines 20, 21 and 26 of the **modified** `xmmatrix.cpp` source code file.

Disabling intrinsics with a define is a **bad** idea, because it slows down your program immensely. Where possible convert your code to correctly load and store intrinsic values, as above.

However, for a '_disabling intrinsics_' solution to the issue of line 22 of the **original** `xmmatrix.cpp` source code file, try defining `_XM_NO_INTRINSICS_` in the pre-processor directive of the C++ entry of your project properties, or `#define _XM_NO_INTRINSICS_` before you `#include` any DirectX headers.

For example, add `#define _XM_NO_INTRINSICS_` at the head of the file:

`#include <windows.h>`
`#define _XM_NO_INTRINSICS_  // Must be before #include <DirectXMath.h>`
`#include <DirectXMath.h>`
`#include <iostream>`

Check out other alternative solutions for the issue at [Access floats of XMMatrix - () operator not working
](https://stackoverflow.com/questions/17475929/access-floats-of-xmmatrix-operator-not-working).
