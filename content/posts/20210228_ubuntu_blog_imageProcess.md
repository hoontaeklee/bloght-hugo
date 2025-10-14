---
title: "Ubuntu에서 블로그 - 이미지 처리"
author: "Hoontaek Lee"
date: 2021-02-28T20:26:17+01:00
description:
cover: 
  relative: true
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- 2021
- Blog
---

# Ubuntu에서 블로그 - 이미지 처리

블로그에 글을 올리려면 이미지 관련 몇가지 작업을 해야 한다.

다운 받기, 이름 바꾸기, 크기 줄이기, 블로그 폴더에 옮기기...

내 노트북은 이거 하는 데 버벅거린다. 탐색기에서도. 6년 간 혹사시킨 결과.

짱짱한 **연구소 노트북으로 글 쓰기 위해** 저 작업들을 우분투에서 할 방법을 찾아야 했다.

생각보다 쉽게? 어렵게? 물어물어 완성했다.

# Procedure

Rotate (right-clink, manual)

blogImagProcess.sh

1. convert *.png to *.jpg

2. Rename (renameImages.sh)

3. Resize (resizeImages.sh)

# Some details

- rotate image --> nautilus-image-converter
  
  - sudo apt-get install nautilus-image-converter
  - After then, the right-click menu will inclulde **rotate image** and **resize imgae**.

- resize image --> imagemagick
  
  - [imagemagick - How to resize images to either 900-pixels-height for vertical ones or 900-pixels-width for horizontal ones? - Ask Ubuntu](https://askubuntu.com/a/1320060/1180225)

- rename images --> bash
  
  - [bash - Renaming files in a folder to sequential numbers - Stack Overflow](https://stackoverflow.com/a/3211670/7578494)

# Bash files

## blogImgProcess.sh

```bash
bash png2jpg.sh
bash renameImgs.sh
bash resizeImgs.sh
```

## png2jpg.sh

```bash
mogrify -format jpg *.png    
```

## renameImgs.sh

desired format: Jena_wk##_00#.jpg

```bash
a=1
echo -n "enter # of week in Jena: "
read wk
for i in *.jpg; do
  # date=$(date '+%Y%m%d')
  new=$(printf "Jena_wk%s_%03d.jpg" "$wk" "$a")  #04 pad to length of 4
  mv -i -- "$i" "$new"
  let a=a+1
done
```

## resizeImgs.sh

```bash
mogrify -resize 900x900\> *.jpg
```
