---
title: Tips n' Tricks
date: 2022-08-18 23:32:16
---

# Tips n' Tricks

This page contains a collection of all the tips and tricks I use to get my work done faster. I use Debian as my distro as choice so all the commands here will be skewed in favor of it.

## FFMPEG

### Convert MKV to MP4

```bash
	ffmpeg –i input.mkv –c:v h264 output.mp4
```

### Convert MP4 to MP4

```bash
	ffmpeg -i input.mp4 -vn -acodec mp3 -ab 320k -ar 44100 -ac 2 output.mp3
```

### Convert MP4 to WAV

```bash
	ffmpeg -i input.mp4 output.wav
```

### Convert MP4 to PNGs

Output one image every second:

```bash
	ffmpeg -i input.mp4 -vf fps=1 out%d.png
```

Output one image every minute:

```bash
	ffmpeg -i test.mp4 -vf fps=1/60 thumb%04d.png
```

Output one image 10 minutes:

```bash
	ffmpeg -i test.mp4 -vf fps=1/600 thumb%04d.png
```

## Find and Replace

### Find and replace a string with folder exclusions

```bash
	find ./ -type f -not -path '/.' -not -path "./exclude/*" -readable -writable -exec sed -i "s/bad/good/g" {} \;
```

This will exclude all folders starting with './' which includes stuff like .git and also other folders like './exclude/', change to your liking accordingly.

## Node and NPM

### Install nvm

```bash
	curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

## Git

### Initialize and update submodules

```bash
	git submodule update --init
```


### Remove a Submodule

```bash
	git submodule deinit <path_to_submodule>
	git rm <path_to_submodule>
	git commit -m "Removed submodule"
	rm -rf .git/modules/<path_to_submodule>
```

### Cache Authentication token for 20 hours

```bash
	git-credential-manager-core configure
	git config --global credential.credentialStore cache
	git config --global credential.cacheoptions "--timeout 72000"
```

## Convert files

You need `imagemagick` for the `convert` command

```bash
	sudo apt-get install imagemagick
```

### PNGs to JPEGs

```bash
	convert input.png -quality 90 output.jpg
```

To convert all the png files in a directory to jpegs:

```bash
	mogrify -format jpg *.png
```

## Miscellaneous

### Get your current IP address

```bash
	curl icanhazip.com
```

### Rename all the files of an extension in sequential order

```bash
	ls | cat -n | while read n f; do mv "$f" "$n.jpg"; done
```
