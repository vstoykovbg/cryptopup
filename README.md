# Cryptopup
Modified bionicpup64-8.0 with added crypto tools: [doubleslow](https://github.com/vstoykovbg/doubleslow), [doublerandom](https://github.com/vstoykovbg/doublerandom), [RFC1751-encoding-decoding](https://github.com/vstoykovbg/RFC1751-encoding-decoding) and others.

The best way to use this distro is to burn it on a DVD or CD and run it on an air-gapped computer without a hard drive, without a network controllers (especially wireless), without USB devices (especially USB memory sticks, printers, scanners, etc). Ideally the computer must contain only the most important components: power supply, motherboard (with integrated video controller and microphone input), RAM, processor, optical drive. And of course monitor, keyboard and mouse. Also it would be good to have a microphone or a noise generator attached to the microphone input. Connecting USB printer may compromise your secirity. Connecting the computer to other computer after using if for sensitive cryptographic stuff is not recommended.

If you want to transfer data to/from the computer you can use [RFC1751 encoding/decoding](https://github.com/vstoykovbg/RFC1751-encoding-decoding). If you want to print data - use a pencil.

Please be aware that I am a very trustworthy pseudonymous stranger on the Internet, but nevertheless I can't guarantee that there is no malware on this ISO. This distro is based on Puppy Linux (bionicpup64-8.0), which is based on Ubuntu, which is based on Debian... What could go wrong? 

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

## What could go wrong?

If you make sure to seed the PRNG with randomness from the sound input, mouse movements, etc. before using anything crypto-related - maybe it will be ok.

There is a clipboard manager enabled by default:

![screenshot of the clipboard manager](images/clipboard-manager-hmmm.png?raw=true "Clipboard manger. What could go wrong?")

If you run the OS from a hard drive - bad news. Your secrets you are copy/pasting are in cleartext on the hard drive (unless you use full disk encryption, including encrypted swap). And it's difficult to remove it, especially when the hard drive's firmware decided to mark the area as corrupted - it will not be deleted or overwritten with the usual disk wiping tools.

Since you are using the OS from an optical disk on a read-only optical device (not using it on a CD/DVD burner?) and there is no hard drive - nothing could go wrong? Or maybe not? If we asume there is no malware hidden in the BIOS/UEFI, inside the [processor](https://www.google.com/search?channel=fs&client=ubuntu&q=%22Intel+Management+Engine+and+its+applications+are+a+backdoor+with+total+access+to+and+control+over+the+rest+of+the+PC.%22)...

## Download
- IPFS: QmNU2dWgDzre7yd988jRLd8FnfSSqxTg2kEk9JFHFEmDsi
- BitTorrent: magnet:?xt=urn:btih:dfc66c676fcb073da12a34091e4d01bed7d267b9&dn=bionicpup64-8.0-with-crypto-tools
- IPFS gateways: [localhost](http://localhost:8080/ipfs/QmNU2dWgDzre7yd988jRLd8FnfSSqxTg2kEk9JFHFEmDsi), [1](https://gateway.pinata.cloud/ipfs/QmNU2dWgDzre7yd988jRLd8FnfSSqxTg2kEk9JFHFEmDsi), [2](https://ninetailed.ninja/ipfs/QmNU2dWgDzre7yd988jRLd8FnfSSqxTg2kEk9JFHFEmDsi), [3](https://cloudflare-ipfs.com/ipfs/QmNU2dWgDzre7yd988jRLd8FnfSSqxTg2kEk9JFHFEmDsi), [4](https://ipfs.io/ipfs/QmNU2dWgDzre7yd988jRLd8FnfSSqxTg2kEk9JFHFEmDsi), [5](https://dweb.link/ipfs/QmNU2dWgDzre7yd988jRLd8FnfSSqxTg2kEk9JFHFEmDsi)

Long magnet link (with trackers):
```
magnet:?xt=urn:btih:dfc66c676fcb073da12a34091e4d01bed7d267b9&dn=bionicpup64-8.0-with-crypto-tools&tr=udp%3A%2F%2Fwambo.club%3A1337%2Fannounce&tr=udp%3A%2F%2Ftc.animereactor.ru%3A8082%2Fannounce&tr=udp%3A%2F%2Ftracker.justseed.it%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=https%3A%2F%2Fopen.kickasstracker.com%3A443%2Fannounce&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Fopen.stealth.si%3A80%2Fannounce&tr=http%3A%2F%2F87.253.152.137%2Fannounce&tr=http%3A%2F%2F91.217.91.21%3A3218%2Fannounce&tr=http%3A%2F%2Fatrack.pow7.com%2Fannounce&tr=http%3A%2F%2Fbt.henbt.com%3A2710%2Fannounce&tr=http%3A%2F%2Fbt.pusacg.org%3A8080%2Fannounce&tr=https%3A%2F%2Ftracker.bt-hash.com%3A443%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=https%3A%2F%2F182.176.139.129%3A6969%2Fannounce&tr=udp%3A%2F%2Fzephir.monocul.us%3A6969%2Fannounce&tr=https%3A%2F%2Ftracker.dutchtracking.com%3A80%2Fannounce&tr=https%3A%2F%2Fgrifon.info%3A80%2Fannounce&tr=udp%3A%2F%2Ftracker.kicks-ass.net%3A80%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=udp%3A%2F%2Ftracker.sktorrent.net%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.internetwarriors.net%3A1337%2Fannounce&tr=https%3A%2F%2Ftracker.parrotsec.org%3A443%2Fannounce&tr=https%3A%2F%2Ftracker.moxing.party%3A6969%2Fannounce&tr=https%3A%2F%2Ftracker.ipv6tracker.ru%3A80%2Fannounce&tr=udp%3A%2F%2Fopen.stealth.si%3A80%2Fannounce
```


## Official site of Puppy Linux
- http://puppylinux.com/

## Similar projects
- [Bitkey](https://github.com/bitkey/bitkey)
- [Tails](https://tails.boum.org/)
