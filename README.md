[![GoReportCard](http://goreportcard.com/badge/github.com/asticode/go-asticoqui)](http://goreportcard.com/report/github.com/asticode/go-asticoqui)
[![GoDoc](https://godoc.org/github.com/asticode/go-asticoqui?status.svg)](https://godoc.org/github.com/asticode/go-asticoqui)

Golang bindings for Coqui's [:frog:STT](https://github.com/coqui-ai/STT) speech-to-text library.

`asticoqui` is compatible with version `v1.0.0`, `v1.1.0`, and `v1.2.0` of 🐸STT.

# Installation  

## Install tflite

Run the following command:

```bash
    $ pip3 install --extra-index-url https://google-coral.github.io/py-repo/ tflite_runtime
```

If you're interested in running against your CUDA-enabled GPU (optional), then set the environment variable `STT_TFLITE_DELEGATE=gpu`.

## Install Coqui STT

1. fetch an up-to-date `native_client.*.tar.xz` matching your system from [:frog:STT releases](https://github.com/coqui-ai/STT/releases). For example, on macOS:

```bash
    $ wget https://github.com/coqui-ai/STT/releases/download/v1.2.0/native_client.tflite.macOS.tar.xz
```

2. extract its content to `$HOME/.coqui/`. For example, on macOS:

```bash
    $ mkdir $HOME/.coqui/
    $ tar -xvzf native_client.tflite.macOS.tar.xz -C $HOME/.coqui/
```

3. set environment variables to point to client

```bash
    $ export CGO_LDFLAGS="-L$HOME/.coqui/"
    $ export CGO_CXXFLAGS="-I$HOME/.coqui/"
    $ export LD_LIBRARY_PATH="$HOME/.coqui/:$LD_LIBRARY_PATH"
```

## Install asticoqui
### Install dependencies

Run the following command:

```bash
    $ go get -u github.com/asticode/go-asticoqui/...
```

### Install executables

Run the following command:

```bash
    $ go install github.com/asticode/go-asticoqui/cmd
```

# Example usage
## Get the pre-trained model and scorer

Go to [this page](https://coqui.ai/english/coqui/v1.0.0-huge-vocab) and click `Enter Email to Download` at the bottom of the page. Download `model.tflite` and `huge_vocabulary.scorer`.
    
## Get the audio files

Run the following commands: 

```bash
    $ cd $HOME/.coqui
    $ wget https://github.com/coqui-ai/STT/releases/download/v1.2.0/audio-1.2.0.tar.gz
    $ tar -xvfz audio-1.2.0.tar.gz
```

## Use this client

Run the following commands:

```bash
    $ go run coqui/main.go -model model.tflite -scorer huge_vocabulary.scorer -audio audio/2830-3980-0043.wav
    
        Text: experience proves this
    
    $ go run coqui/main.go -model model.tflite -scorer huge_vocabulary.scorer -audio audio/4507-16021-0012.wav
    
        Text: why should one hall on the way
        
    $ go run coqui/main.go -model model.tflite -scorer huge_vobaculary.scorer -audio audio/8455-210777-0068.wav
    
        Text: your power is sufficient i said
```
