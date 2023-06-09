## Implementation of HPPC

Each implementation has its own MAKEFILE that is comprised of the following:
    
- Optimized KAT test values generation. MAKEFILE is tunable you can disable OPTIMIZED flag here
    - KAT Generation time n=128 3min, n=192 9min, n=256 25min
- Unoptimized performance test in single core.
- Optimized performance test in single core.
- Optimized performance with Strassen multiplication that may run in parallel depending of the situation (handled by M4RI library internally).

Each algorithm has its tunable parameters in api.h

- N is the dimension of the finite field.
- d is the exponent for calculating the degree of the private polynomial 2^d + 1 for d=10,D=1025.
- VIN_VARS are the vinegar variables, here 1 byte.

Used files in the implementations are:

- gen.c, gen.h: For generating the Public and Private key.
- serializer.c, serializer.h: Encoding and Decoding of Public and Private key.
- sign.c: For message signing and signature verification.
- ntl_utils.cpp, ntl_utils.h: NTL code for finding roots of a polynomial over a Finite field extension. Coded in C++ so linked with C by extern "C" definition.
- MAKEFILE: For building KAT and performance testing binaries.

Reference and Optimized implementations are both the same.

In Third Party libraries you will found libraries used by the implementations that are not covered by NIST in the FAQs. These are:
    
- FLINT
- M4RI

Only NTL is covered by NIST, so it's presumed that it's already installed as a library. FLINT and M4RI are easily compiled and installed manually, or by downloading them from the distribution repository in the case of GNU/Linux or UNIX based OS.

Please read the attached INSTALL file carefully.