# btc_p2kh_addrgen
Bitcoin p2kh address priv/pub key pair generator

Generate your own private key (5 lines of python)
//# pip install base58 / ecdsa
//# tested in python 3.6.5

  // import os, binascii, hashlib, base58
  // fullkey = "80"+ binascii.hexlify(os.urandom(32)).decode()
  // sha256a = hashlib.sha256(binascii.unhexlify(fullkey)).hexdigest()
  // sha256b = hashlib.sha256(binascii.unhexlify(sha256a)).hexdigest()
  // WIF = base58.b58encode(binascii.unhexlify(fullkey+sha256b[:8]))
  // print(WIF)

A few lines of python... perhaps useful for the paranoid.
E.g. - easy to run this on disconnected bootable thumb drive.

ref. https://bitcoin.stackexchange.com/questions/65652/ecdsa-create-private-key-and-bitcoin-address


one comment, which is on my part 50% irresponsible, and 50% OCD... I prefer to leave out the "fit" to ecdsa check, because it eliminates 4 lines of code even if it does expose you to 1-in-zillion(?) chance of producing invalid address.

using urandom might not be secure and could possibly generate predictable keys... I would be careful doing that.

urandom actually....

https://docs.python.org/2/library/os.html#os.urandom

    Return a string of n random bytes suitable for cryptographic use.

    This function returns random bytes from an OS-specific randomness source. The returned data should be unpredictable enough for cryptographic applications, though its exact quality depends on the OS implementation. On a UNIX-like system this will query /dev/urandom, and on Windows it will use CryptGenRandom().

Again - the paranoid(wise) should never connect computer that generates keys to a network... after it's generated keys, in case of spyware.

You don't. It relies on base58, which is not part of the python standard library. You'd most likely download and install it from PyPI. In theory, that library could be changed at any time by whoever uploaded it so that it does something totally different next time you update your libs with pip. What you install is not necessarily what is hosted on the github repo, nor does PyPI provide any kind of guarantee that the uploader is who they say they are. And many people run pip install as root too, so you're giving root access to the package maintainer.

It might be totally fine. It might not. It might be fine today, and not fine next time you upgrade your system.

And if not it wouldn't be the first time spoof libs have been uploaded there and installed by unwitting Devs who blindly trust external software repos that allow contributions by anyone. PyPI has very few checks and balances compared to other repos like Linux package repos, maven etc. No mandatory PKI keys/sigs, mentoring, or community standards, or anything really. All you need to upload a package is a working email address.
