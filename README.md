# dawn-signed
Collection of signed builds of wine and dxvk for certain anime games

The CA certificates used for signing the builds are in the CA directory.

## DXVK

Useful for a certain honkers railway, the game does not require a patch where this is installed.
The other games by the same Anime Game Company should not complain when running on such a prefix,
it is your choice whether to use it or not as both sides of the coin has valid arguments.

Binaries are sourced directly from [upstream](https://github.com/doitsujin/dxvk), it is possible
to verify the authenticity of these builds by comparing the section content of the binary with 
the upstream builds. Note that comparing raw data of signature-removed binaries will **NOT** yield
the same hashes.

### Installation

1. Download a dxvk-dw build from the releases on this repo
2. Install dxvk-dw same as upstream, copy x64 contents into `C:\windows\system32`, x32 into `C:\windows\syswow64`.
3. Add wine DLL overrides for `d3d8`, `d3d9`, `d3d10core`, `d3d11`, and `dxgi` in `winecfg`
4. Open `wine control`, Internet Settings -> Content -> Certificates
    1. Navigate to "Trusted Root Certification Authorities"
    2. Click Import
    3. Follow wizard, select the "ca-root.crt" when prompted, leave remaining settings as is, and finish.
    4. Navigate to "Intermediate Certification Authorities"
    5. Click Import
    6. Follow wizard, select "interm.crt" when prompted, leave remaining settings as is and finish.
5. Navigate to `C:\windows\system32\catroot\{127d0a1d-4ef2-11d1-8608-00c04fc295ee}`
    1. If the folder does not exist, create it
    2. Copy DXVK.cat to folder

### Verifying

If you are interested in verifying the signatures in the binary, it is possible to do so with `osslsigncode` 
on linux, the code signing certificate `CA/dawncodesign.crt` is provided, in order to check, the signature 
on a release binary, you can use the commands:
```bash
cat CA/ca-root.crt CA/interm.crt > chain.crt
osslsigncode verify -in <binary> -c <catalog> -CAfile chain.crt
```
# Wine

Required for a certain anime game.

## Installation

1. Open `wine control`, Internet Settings -> Content -> Certificates
    1. Navigate to "Trusted Root Certification Authorities"
    2. Click Import
    3. Follow wizard, select the "ca-root.crt" when prompted, leave remaining settings as is, and finish.
2. Install the signed dxvk (also can be found in the dawn-signed repo) using
it's readme, skipping the installation of the  ca-root.crt has it has 
already been installed here in step 1.
3. With the prefix setup game can be run normally.

Note: The Anime Game may kick you out one or two times, by the third time it
should accept and proceed.
