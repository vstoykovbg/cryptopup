# Cryptopup

Cryptopup is a live Linux distribution that fits on a CD (it's only 531MiB) but also can be burned on a DVD or recorded on a USB flash drive. It contains useful crypto tools: [Doubleslow](https://github.com/vstoykovbg/doubleslow), [Doublerandom](https://github.com/vstoykovbg/doublerandom), [RFC1751-encoding-decoding](https://github.com/vstoykovbg/RFC1751-encoding-decoding), [Mnemonic hashes](https://github.com/vstoykovbg/mnemonic-hashes), Electrum, Bitaddress, [BIP39 tool](https://github.com/iancoleman/bip39) and others.

When text mode is selected (with "do not copy in RAM") it requires very low RAM (assuming you will use frugal settings on Doubleslow). I tested it with 192MB RAM and Doubleslow was able to work with 64MiB RAM requirement for the first stage of hashing.

![Cryptopup boot screen](images/cryptopup_11.png?raw=true "Cryptopup boot screen")

In the following example it works with only 192MB RAM (in Linux console mode, selected as shown in the above screenshot).

![My horse eats batteries](images/horse_1.png?raw=true "My horse eats batteries and works with only 192MB RAM")

In this example the salt is `my horse eats batteries`, the password is `123`, the number of iterations on the first stage is `5`, there is no second stage. These are very weak settings, do not use it like this.

![The result of the Doubleslow key stretching](images/horse_2.png?raw=true "The result of the Doubleslow key stretching")

Cryptopup is based on BionicPup64 8.0.

The best way to use this distro is to burn it on a DVD or CD and run it on an air-gapped computer without a hard drive, without wireless network controllers, without USB devices (especially USB memory sticks, printers, scanners, etc). Ideally the computer must contain only the most important components: power supply, motherboard (with integrated video controller and microphone input), RAM, processor, optical drive. And of course monitor, keyboard and mouse. Also it would be good to have a microphone or a noise generator attached to the microphone input. Connecting an USB printer may compromise your security. Connecting the computer to other computer after using if for sensitive cryptographic stuff is not recommended (what if there is a crypto keys stealing malware hidden inside the BIOS/UEFI?).

If you want to transfer data to/from the computer you can use [RFC1751 encoding/decoding](https://github.com/vstoykovbg/RFC1751-encoding-decoding). If you want to print data - use a pencil.

![Cryptopup with Veracrypt, mouse-seed-generator.py, mnemonic-blake.py ](images/cryptopup_vera.png?raw=true "Cryptopup with Veracrypt, mouse-seed-generator.py, mnemonic-blake.py")

Please be aware that I am a very trustworthy pseudonymous stranger on the Internet, but nevertheless I can't guarantee that there is no malware on this ISO. If we assume that there is no malware in Ubuntu and BionicPup64, it's very probable that there is no malware in Cryptopup. 

If you plan to use crypto tools for critical applications - make your own live distro, do not trust a random stranger on the Internet to make it for you. This type of software (wallet generators, BIP39 tools, etc) is a magnet for criminals.

- [Looking for BIP39 tools? Beware of phishing!](https://rootvideochannel.blogspot.com/2020/10/looking-for-bip39-tools-beware-of.html)
- [Just saw this suspicious advertisement on Facebook for www.ethpaperwallet.net - phishing website](https://rootvideochannel.blogspot.com/2017/12/just-saw-this-suspicious-advertisement.html)
- [Example of "phishing" Bitcoin wallet generator - walletgenerator.org](https://rootvideochannel.blogspot.com/2017/12/example-of-phishing-bitcoin-wallet.html)
- [Suspicious website cryptocurrencysecurityadvice.com - probably hosting malware](https://rootvideochannel.blogspot.com/2017/12/suspicious-website-cryptocurrencysecuri.html)
- [Stealing Bitcoin "is nothing illegal, but morally wrong" - WTF?](https://rootvideochannel.blogspot.com/2017/12/stealing-bitcoin-is-nothing-illegal-but.html)

## Where are the crypto tools?

The most interesting stuff is in the /opt directory:

- /opt/my-apps/doubleslow
- /opt/my-apps/doublerandom
- /opt/my-apps/RFC1751-encoding-decoding-master
- /opt/my-apps/mnemonic-hashes
...

## What could go wrong?

If you make sure to seed the PRNG with randomness from the sound input, mouse movements, etc. before using anything crypto-related - maybe it will be ok.

There is a clipboard manager enabled by default:

![screenshot of the clipboard manager](images/clipboard-manager-hmmm.png?raw=true "Clipboard manger. What could go wrong?")

If you run the OS from a hard drive - bad news. Your secrets you are copy/pasting are in cleartext on the hard drive (unless you use full disk encryption, including encrypted swap). And it's difficult to wipe the secrets, especially when the hard drive's firmware decided to mark the area as corrupted - it will not be deleted or overwritten with the usual disk wiping tools.

Since you are using the OS from an optical disk on a read-only optical device (not using it on a CD/DVD burner?) and there is no hard drive - nothing could go wrong, right? Or maybe not? If we assume there is no malware hidden in the BIOS/UEFI, inside the [processor](https://www.google.com/search?channel=fs&client=ubuntu&q=%22Intel+Management+Engine+and+its+applications+are+a+backdoor+with+total+access+to+and+control+over+the+rest+of+the+PC.%22)...

Please read the code of the randomness mixers before using them. Be skeptical to any BIP39 mnemonic generator, wallet generator, etc. Does it produce really random output? Or it's rigged in a way someone can abuse? Does it transmit the generated seeds and keys to the mothership?

For ideas how things could go wrong - read the README.md from the [Doubleslow](https://github.com/vstoykovbg/doubleslow) project.

## What is changed?

Mostly my changes are installing dependencies of the crypto-tools I added in the /opt directory. I had difficulties with compiling software on the Puppy, so I compiled the software on my Ubuntu system (`$ make`, `$ python3 setup.py build`) and then installed it (i.e. `# python3 setup.py install`) on the Puppy system. This way I installed VeraCrypt and the Python modules `pynput` and `argon2`.

I added a new entry in the `isolinux.cfg` menu "without graphical desktop, do not copy in RAM". It's useful on old computers with low RAM.

I made changes in the keyboard settings in the text mode (Linux console) - with Ctrl+Shift a Bulgarian phonetic layout can be selected. The default is US layout.

I did not liked how `xvcbd` beeps when keys are pressed (it's using the system speaker for this) and not showing cyrillic letters when I change the keyboard layout, so I installed `onboard` (Gnome's onscreen keyboard). Virtual keyboards are useful to reduce the risk of keylogging attacks.

Your keyboard or BIOS/UEFI can be infected with a hardware or a software keylogger.

It's more difficult to steal secrets by recording the mouse movements than by recording the pressed keys on the physical keyboard.

The hypothetical malware can write your secrets on the memory of your USB devices in a way you can't read them, but the attacker can. This is why I suggest to avoid USB keyboards (you may accidentally attach the same keyboard on an online computer, and - it's_gone_meme.jpg - if we assume the malware on the online computer cooperate with the malware on the keyboard's controller).

## Download Cryptopup 11
- [https://drive.google.com/drive/folders/1O1AJU895hcuQkCiruNdlWn46rKB4WTOm?usp=sharing]Google Drive]
- IPFS: Qmf8JcNDaaiKkunvnE2mfDQCW1qrczKmDtt4ReNvbXDpMM
- BitTorrent: magnet:?xt=urn:btih:667c4081b98970bf21066978d97ca93ea24cd6ee&dn=cryptopup%5F11
- IPFS gateways: [localhost](http://localhost:8080/ipfs/Qmf8JcNDaaiKkunvnE2mfDQCW1qrczKmDtt4ReNvbXDpMM), [1](https://gateway.pinata.cloud/ipfs/Qmf8JcNDaaiKkunvnE2mfDQCW1qrczKmDtt4ReNvbXDpMM), [2](https://ninetailed.ninja/ipfs/Qmf8JcNDaaiKkunvnE2mfDQCW1qrczKmDtt4ReNvbXDpMM), [3](https://cloudflare-ipfs.com/ipfs/Qmf8JcNDaaiKkunvnE2mfDQCW1qrczKmDtt4ReNvbXDpMM), [4](https://ipfs.io/ipfs/Qmf8JcNDaaiKkunvnE2mfDQCW1qrczKmDtt4ReNvbXDpMM), [5](https://dweb.link/ipfs/Qmf8JcNDaaiKkunvnE2mfDQCW1qrczKmDtt4ReNvbXDpMM)

Long magnet link (with trackers):
```
magnet:?xt=urn:btih:667c4081b98970bf21066978d97ca93ea24cd6ee&dn=cryptopup%5F11&tr=udp%3A%2F%2Fwambo.club%3A1337%2Fannounce&tr=udp%3A%2F%2Ftc.animereactor.ru%3A8082%2Fannounce&tr=udp%3A%2F%2Ftracker.justseed.it%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=https%3A%2F%2Fopen.kickasstracker.com%3A443%2Fannounce&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Fopen.stealth.si%3A80%2Fannounce&tr=http%3A%2F%2F87.253.152.137%2Fannounce&tr=http%3A%2F%2F91.217.91.21%3A3218%2Fannounce&tr=http%3A%2F%2Fatrack.pow7.com%2Fannounce&tr=http%3A%2F%2Fbt.henbt.com%3A2710%2Fannounce&tr=http%3A%2F%2Fbt.pusacg.org%3A8080%2Fannounce&tr=https%3A%2F%2Ftracker.bt-hash.com%3A443%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=https%3A%2F%2F182.176.139.129%3A6969%2Fannounce&tr=udp%3A%2F%2Fzephir.monocul.us%3A6969%2Fannounce&tr=https%3A%2F%2Ftracker.dutchtracking.com%3A80%2Fannounce&tr=https%3A%2F%2Fgrifon.info%3A80%2Fannounce&tr=udp%3A%2F%2Ftracker.kicks-ass.net%3A80%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=udp%3A%2F%2Ftracker.sktorrent.net%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.internetwarriors.net%3A1337%2Fannounce&tr=https%3A%2F%2Ftracker.parrotsec.org%3A443%2Fannounce&tr=https%3A%2F%2Ftracker.moxing.party%3A6969%2Fannounce&tr=https%3A%2F%2Ftracker.ipv6tracker.ru%3A80%2Fannounce&tr=udp%3A%2F%2Fopen.stealth.si%3A80%2Fannounce
```
## Known bugs

One of the files (`initrd.gz`) was changed after computing the checksums.

## Official site of Puppy Linux
- http://puppylinux.com/

## Similar projects
- [Bitkey](https://github.com/bitkey/bitkey)
- [Tails](https://tails.boum.org/)
