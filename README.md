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
