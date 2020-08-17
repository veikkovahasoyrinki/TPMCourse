# Platform Configuration Registers
- [Platform Configuration Registers](#platform-configuration-registers)
  - [Reading PCRs](#reading-pcrs)
    - [Reading all PCRs from all banks](#reading-all-pcrs-from-all-banks)
    - [Reading a set of PCRs](#reading-a-set-of-pcrs)
    - [Reading a single bank of PCRs](#reading-a-single-bank-of-pcrs)
  - [Extending PCRs](#extending-pcrs)
  - [Resetting a PCR](#resetting-a-pcr)
  - [Extending a PCR with the hash of file](#extending-a-pcr-with-the-hash-of-file)

The TPM contains a number of banks of registers used for storing measurements - typically of boot time measurements.

The TCG TPM 2.0 standard states that there must be at least two banks, one SHA1 and one SHA256, containing 24 registers

The TCG x86 Boot Standard states that some of these registers are to be populated during a trusted boot (on x86) and certain registers are used for specific purposes, eg: CRTM, BIOS measures.

## Reading PCRs

### Reading all PCRs from all banks
```bash
[fedora@vm021273 ~]$ tpm2_pcrread
sha1:
  0 : 0x7EBA0CFB74F41FEBCCDD1251F02BC208052B6023
  1 : 0xB8720B5234E2F08CFA87069F172CBB43F0F08225
  2 : 0x86FA03B9C721AF57DE8FB1C43CC3FE7B0A42239A
  3 : 0xB2A83B0EBF2F8374299A5B2BDFC31EA955AD7236
  4 : 0xAB705AAE41789E02A1909B2CBB8BFC0806115004
  5 : 0x7B25D2EABBA18DC910E724A0C75020F1FEC80BE2
  6 : 0xB2A83B0EBF2F8374299A5B2BDFC31EA955AD7236
  7 : 0x518BD167271FBB64589C61E43D8C0165861431D8
  8 : 0xC3DF1A5D37AC51163C63320F28B9C1C1FD933BD2
  9 : 0x944C3EFEB668CB217B260F7D4B594DA4341E6FF2
  10: 0xA3500BFF7A194B447D7FE57A089DED8D29581DBE
  11: 0x0000000000000000000000000000000000000000
  12: 0x0000000000000000000000000000000000000000
  13: 0x0000000000000000000000000000000000000000
  14: 0x0000000000000000000000000000000000000000
  15: 0x0000000000000000000000000000000000000000
  16: 0x0000000000000000000000000000000000000000
  17: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  18: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  19: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  20: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  21: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  22: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  23: 0x0000000000000000000000000000000000000000
sha256:
  0 : 0xDE7022997F99B5DB26C9D64FB4C7AB83A1B1FAAAC24FF3E3936F002F3A53BD9B
  1 : 0x0E45F4E9217FF2305B599C74C005B5F20C40515E063A5077CAA0310D4209D527
  2 : 0x28D1B29995FDB6288D86B5905E79002B35F24705437FE62AD57293CD04FDBAA6
  3 : 0x3D458CFE55CC03EA1F443F1562BEEC8DF51C75E14A9FCF9A7234A13F198E7969
  4 : 0xE7BD29E5572B42709E0F6EAB4423713D3424A5CD3221EBF49721DCC909FA9001
  5 : 0xB6E968CD86966C6B3DEAC77B2E7613DC414CFA5B99598209B321D0DFD6CCB864
  6 : 0x3D458CFE55CC03EA1F443F1562BEEC8DF51C75E14A9FCF9A7234A13F198E7969
  7 : 0x65CAF8DD1E0EA7A6347B635D2B379C93B9A1351EDC2AFC3ECDA700E534EB3068
  8 : 0x56ABAC0E1C907D7CBF58EE60AB68538F727F6AC116C8785B67C07E39A1AD3F27
  9 : 0x5EAE243245C62F9AD0528CC7858C4366C7891AB4615132F206077C49A8838DA9
  10: 0x8848D3C10FB47F4073A2F06C03300294412D07245BD06DCEDDECAC71C31B6F2C
  11: 0x0000000000000000000000000000000000000000000000000000000000000000
  12: 0x0000000000000000000000000000000000000000000000000000000000000000
  13: 0x0000000000000000000000000000000000000000000000000000000000000000
  14: 0x0000000000000000000000000000000000000000000000000000000000000000
  15: 0x0000000000000000000000000000000000000000000000000000000000000000
  16: 0x0000000000000000000000000000000000000000000000000000000000000000
  17: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  18: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  19: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  20: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  21: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  22: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  23: 0x0000000000000000000000000000000000000000000000000000000000000000
sha384:
  0 : 0x3107B2455FCE38B2779296D0A8B951AA9DA268D36AF270B0E38E84D4FA8EBAE25E4191CB5490BF00A1C6E94BBE2BC03E
  1 : 0x6594397CDB6033A406E349FEED7836BF02DD1D574C724660BE8BA0E82627768D1333F835B2FF8D006F0BEE6A6152223D
  2 : 0xDCD2E666AC30040F3BFA1E7C8F546FEBC94DBFF78831D8A4DF310DE2105FE3F0E0088FDC668137A36831C4D64737A78D
  3 : 0x518923B0F955D08DA077C96AABA522B9DECEDE61C599CEA6C41889CFBEA4AE4D50529D96FE4D1AFDAFB65E7F95BF23C4
  4 : 0xEE0507B6B5A3DB4477DFE08CD16E6C616FAE7A76CBC074719B9410D435FFF2E539249E7A4AC50C1C27F780B046DE5698
  5 : 0xA553D02AC8C368C6930A3DF65EF9E62A4E575270A9BDEB7968C0E2E1BF754A924E0EDFE932FFD4A00CE214B9C3A10A7E
  6 : 0x518923B0F955D08DA077C96AABA522B9DECEDE61C599CEA6C41889CFBEA4AE4D50529D96FE4D1AFDAFB65E7F95BF23C4
  7 : 0x98441C7F7625D10058C47683AEC486CE311C633235EB555593A7EE791121E3578AE72D04ECEF661F272D59058B77AF35
  8 : 0xB8D008A7BF95B99ADD4764A35F17E5861E47D3FE408B419BC3F06E56D88B419F61E56F60AB16EECCE3BF39542E8E63BC
  9 : 0x0D16C863CBFFAA0CD007FA978CB6D6730710FB68FA5670E18EE14A6C5DDA0DD60058125484E1153479A6B3AE84196DC2
  10: 0x5C58E808B7B40D97A4A7EAD5E70A8E4CB00A74A595B2F3EC7D021110C30A09B7A5823503EB5A217193DED5D9ED905B32
  11: 0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  12: 0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  13: 0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  14: 0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  15: 0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  16: 0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  17: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  18: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  19: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  20: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  21: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  22: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  23: 0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
sha512:
  0 : 0x45826319AE145538E1F5313E5858D6575F527E0A9FF87B6979F896A7D3C4D596255C9CE6CDB822CD50716490340F2091E2021CF23445A00262EB21C7CB9A1E31
  1 : 0x8B0A84F288E65721005ED74380FA6C0A9845736DFA555476B5CBE7610558C087DEF937F06F10CCFCC0DC405D2C4EBFCB8478EA1329589CC27DC38632A5F273B9
  2 : 0xE4D3BD4A23871FEC350D4FCB362D90E3C3EE341D4AEB09B19AFF0E6CC82FC36F2CAD7DD8EF54A681D02F77F7EFDF68AF1274BBFD1C46A1DCF63691E9A6E09E22
  3 : 0x27EC091533C4B9EEA38DD14C3A3ECDEF0A99C1E564CBE66DFE008250154E7839B0B75228FE8DEBCC4CA330E6AEBC1ABC74070BC9C9C1E26B939C9D916E45E13C
  4 : 0x7E4EB1A1758187BB11162D04643C26C62FC7B2D743FDDD058021DA727DD0D61A6263A6FD8D10789566BB1F63EA9253E96AF5944E8F5B8DB17E04F2F4EA162672
  5 : 0x0CF5C79591EB7218276AF2EC0C18C891568912D946AC9C8F2693E77CAA7B16368F7E5B2C117DF92E75286A4436575276C26032979BB097ED8AB5329C2C04A414
  6 : 0x27EC091533C4B9EEA38DD14C3A3ECDEF0A99C1E564CBE66DFE008250154E7839B0B75228FE8DEBCC4CA330E6AEBC1ABC74070BC9C9C1E26B939C9D916E45E13C
  7 : 0x7793D61D41CF40AE7CBF782DCAC336AB5D8546D8B6C369FBA740C784E16D4EC83247AF2043F6352790A9EB9AAB9C95EF318E5DD22C788E0848A10F8C87472A3E
  8 : 0xA8A3D62463B3FF6C334B60A7CB3BA20D2FC1A1A70F6BA3AAFF473AD5654A3BCF9DA136DBC4328AAA5D1D229FB45CA8AE48804E9E76FA08469D3BCB54666590EE
  9 : 0xC004F7B3BAC29026C84845599D78672FCCAFB22F9D99997F33E7AF78B5ACB86D520CA2D7C3C37CE88B4AB6F52607D40785AC9AF00C98F6B59216056BFECC52DB
  10: 0x76153EAA35A8313E8CBE51CE540B5BEE5CC6FF1894D5EC0C2A0902FA7FF3ACBE573346C2695EA358B9006D10DDCACBB23A02604F423A160D8170640E61066A21
  11: 0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  12: 0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  13: 0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  14: 0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  15: 0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  16: 0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
  17: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  18: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  19: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  20: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  21: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  22: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  23: 0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
```

### Reading a set of PCRs
```bash
[fedora@vm021273 ~]$ tpm2_pcrread sha1:0+sha256:0+sha384:0+sha512:0
sha1:
  0 : 0x7EBA0CFB74F41FEBCCDD1251F02BC208052B6023
sha256:
  0 : 0xDE7022997F99B5DB26C9D64FB4C7AB83A1B1FAAAC24FF3E3936F002F3A53BD9B
sha384:
  0 : 0x3107B2455FCE38B2779296D0A8B951AA9DA268D36AF270B0E38E84D4FA8EBAE25E4191CB5490BF00A1C6E94BBE2BC03E
sha512:
  0 : 0x45826319AE145538E1F5313E5858D6575F527E0A9FF87B6979F896A7D3C4D596255C9CE6CDB822CD50716490340F2091E2021CF23445A00262EB21C7CB9A1E31
```

### Reading a single bank of PCRs
```bash
[fedora@vm021273 ~]$ tpm2_pcrread sha1
sha1:
  0 : 0x7EBA0CFB74F41FEBCCDD1251F02BC208052B6023
  1 : 0xB8720B5234E2F08CFA87069F172CBB43F0F08225
  2 : 0x86FA03B9C721AF57DE8FB1C43CC3FE7B0A42239A
  3 : 0xB2A83B0EBF2F8374299A5B2BDFC31EA955AD7236
  4 : 0xAB705AAE41789E02A1909B2CBB8BFC0806115004
  5 : 0x7B25D2EABBA18DC910E724A0C75020F1FEC80BE2
  6 : 0xB2A83B0EBF2F8374299A5B2BDFC31EA955AD7236
  7 : 0x518BD167271FBB64589C61E43D8C0165861431D8
  8 : 0xC3DF1A5D37AC51163C63320F28B9C1C1FD933BD2
  9 : 0x944C3EFEB668CB217B260F7D4B594DA4341E6FF2
  10: 0xA3500BFF7A194B447D7FE57A089DED8D29581DBE
  11: 0x0000000000000000000000000000000000000000
  12: 0x0000000000000000000000000000000000000000
  13: 0x0000000000000000000000000000000000000000
  14: 0x0000000000000000000000000000000000000000
  15: 0x0000000000000000000000000000000000000000
  16: 0x0000000000000000000000000000000000000000
  17: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  18: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  19: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  20: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  21: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  22: 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
  23: 0x0000000000000000000000000000000000000000
```

## Extending PCRs
This is how you add information to a PCR.
First, let's check the contents of the PCR:

```bash
[fedora@vm021273 ~]$ tpm2_pcrread sha1:23
sha1:
  23: 0x0000000000000000000000000000000000000000
```

We can extend with a random hash
```bash
[fedora@vm021273 ~]$ tpm2_pcrextend 23:sha1=f1d2d2f924e986ac86fdf7b36c94bcdf32beec15
```

After extending, we can see that the PCR contents have changed.
```bash
[fedora@vm021273 ~]$ tpm2_pcrread sha1:23
sha1:
  23: 0x3D96EFE6E4A9ECB1270DF4D80DEDD5062B831B5A
```

Note that the contents of the PCR are not exactly the hash we extended, this is because we cannot write directly to the PCR, instead the PCR contents will be the result of concatenating the existing value with the new value and hashing it.
In this case:
```
PCR23 = hash(0x0000000000000000000000000000000000000000, 0xf1d2d2f924e986ac86fdf7b36c94bcdf32beec15)
```

The `hash` function will depend on the bank being extended.
For this case it will be: sha1, sha256, sha384 and sha512.
In some TPMs only the sha1 and sha256 banks are available.


## Resetting a PCR

Only PCR 23 (and sometimes 16) can be reset.
The rest of the PCRs are only resettable on reboot.
This is to prevent a malicious entity from resettting the PCRs that store firmware and boot time measurements and storing fake measurements to trick a verifier into believing the platform is in a good state even though it's not.

Let's check what's on PCR 23:
```bash
[fedora@vm021273 ~]$ tpm2_pcrread sha1:23
sha1:
  23: 0x3D96EFE6E4A9ECB1270DF4D80DEDD5062B831B5A
```

Now, after reset, PCR 23 is emtpy again.

```bash
[fedora@vm021273 ~]$ tpm2_pcrreset 23
[fedora@vm021273 ~]$ tpm2_pcrread sha1:23
sha1:
  23: 0x0000000000000000000000000000000000000000
```

If we try resetting a different PCR, there will be an error and the PCR won't be reset:
```bash
[fedora@vm021273 ~]$ tpm2_pcrread sha1:2
sha1:
  2 : 0x86FA03B9C721AF57DE8FB1C43CC3FE7B0A42239A
[fedora@vm021273 ~]$ tpm2_pcrreset 2
WARNING:esys:src/tss2-esys/api/Esys_PCR_Reset.c:283:Esys_PCR_Reset_Finish() Received TPM Error 
ERROR:esys:src/tss2-esys/api/Esys_PCR_Reset.c:98:Esys_PCR_Reset() Esys Finish ErrorCode (0x00000907) 
ERROR: Could not reset PCR index: 2
ERROR: Esys_PCR_Reset(0x907) - tpm:warn(2.0): bad locality
ERROR: Unable to run tpm2_pcrreset
[fedora@vm021273 ~]$ tpm2_pcrread sha1:2
sha1:
  2 : 0x86FA03B9C721AF57DE8FB1C43CC3FE7B0A42239A
```

## Extending a PCR with the hash of file

We can also extend a PCR with the hash of a file.
The TPM tools have a command that supports hashing a file and extending this hash to a specific PCR.
This makes it so that we don't have to do the hashing and extension operations manually, instead it does it all in one go.

Let's try this with PCR 23 (which we just reset).

We create a file data, which contains a string, e.g. "foo".

```bash
[fedora@vm021273 ~]$ echo "foo" > data
[fedora@vm021273 ~]$ cat data
foo
```

Now, let's extend PCR 23 with the hash of the file `data`:

```bash
[fedora@vm021273 ~]$ tpm2_pcrread sha1:23+sha256:23+sha384:23+sha512:23
sha1:
  23: 0x0000000000000000000000000000000000000000
sha256:
  23: 0x0000000000000000000000000000000000000000000000000000000000000000
sha384:
  23: 0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
sha512:
  23: 0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
```
```bash
[fedora@vm021273 ~]$ tpm2_pcrevent 23 data
sha1: f1d2d2f924e986ac86fdf7b36c94bcdf32beec15
sha256: b5bb9d8014a0f9b1d61e21e796d78dccdf1352f23cd32812f4850b878ae4944c
sha384: 8effdabfe14416214a250f935505250bd991f106065d899db6e19bdc8bf648f3ac0f1935c4f65fe8f798289b1a0d1e06
sha512: 0cf9180a764aba863a67b6d72f0918bc131c6772642cb2dce5a34f0a702f9470ddc2bf125c12198b1995c233c34b4afd346c54a2334c350a948a51b6e8b4e6b6
```
```bash
[fedora@vm021273 ~]$ tpm2_pcrread sha1:23+sha256:23+sha384:23+sha512:23
sha1:
  23: 0x3D96EFE6E4A9ECB1270DF4D80DEDD5062B831B5A
sha256:
  23: 0x44F12027AB81DFB6E096018F5A9F19645F988D45529CDED3427159DC0032D921
sha384:
  23: 0x62EF60F823B16D7757851310525B8AC2927760AFDCB00382110157D81B449B1F7B559A920AF05AA8B28E5BF089A180DB
sha512:
  23: 0x53E36C44309E1FD589FA9495BD2ABF31794DCC6E2E2F65C20DB9ED875A583B0825440923E57E557B28A71F59AA9A3195BAC966F825E3F6D7273B8100A3FD1895
```