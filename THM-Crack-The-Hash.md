# THM - Crack The Hash

[TryHackMe | Crack The Hash](https://tryhackme.com/room/crackthehash)

> Michael Jack | 06/2022

---

## Task 1 - Level 1

### Questions

[Crackstation](https://crackstation.net/)

> 48bb6e862e54f2a795ffc4e541caed4d

```
easy
```

> CBFDAC6008F9CAB4083784CBD1874F76618D2A97

```
password123
```

> 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032

```
letmein
```

> $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom

```shell
hashcat -a 0 -m 3200 '$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom' 4char_rockyou.txt

$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom:bleh
```

```
bleh
```

> 279412f945939ba78ce0758d3fd83daa

```
Eternity22
```

---

## Task 2 - Level 2

> This task increases the difficulty. All of the answers will be in the classic [rock you](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) password list.
> You might have to start using hashcat here and not online tools. It might also be handy to look at some example hashes on [hashcats page](https://hashcat.net/wiki/doku.php?id=example_hashes).

> F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85

```
paule
```

> 1DFECA0C002AE40B8619ECF94819CC1B

```
n63umy8lkf4i
```

> Hash:`$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.`
> Salt: aReallyHardSalt

*Note: Make sure to include the "." at the end!!!*

```shell
hashcat -a 0 -m 1800 hashfile.txt rockyou.txt
```

```
$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.:waka99
```

```
waka99
```

> Hash: e5d8870e5bdd26602cab8dbe07a942c8669e56d6
> Salt: tryhackme

```shell
hashcat -a 0 -m 160 "e5d8870e5bdd26602cab8dbe07a942c8669e56d6:tryhackme" rockyou.txt
```

```
e5d8870e5bdd26602cab8dbe07a942c8669e56d6:tryhackme:481616481616
```

```
481616481616
```

---
