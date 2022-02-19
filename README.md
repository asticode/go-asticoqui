[![GoReportCard](http://goreportcard.com/badge/github.com/asticode/go-asticoqui)](http://goreportcard.com/report/github.com/asticode/go-asticoqui)
[![GoDoc](https://godoc.org/github.com/asticode/go-asticoqui?status.svg)](https://godoc.org/github.com/asticode/go-asticoqui)

Golang bindings for Coqui's [STT](https://github.com/coqui-ai/STT) speech-to-text library.

`asticoqui` is compatible with version `v1.0.0` of `STT`.

# Installation  

## Install tflite

Run the following command:

    $ pip3 install --extra-index-url https://google-coral.github.io/py-repo/ tflite_runtime

to run against gpu set environment variable STT_TFLITE_DELEGATE=gpu (make sure cuda is installed)

## Install Coqui STT

- fetch an up-to-date `native_client.<your system>.tar.xz` matching your system from ["releases"](https://github.com/coqui-ai/STT/releases/tag/v1.0.0)
- extract its content to /tmp
- set environment variables to point to client
    export CGO_LDFLAGS="-L/tmp/native_client.tflite.Linux/"
    export CGO_CXXFLAGS="-I/tmp/native_client.tflite.Linux/"
    export LD_LIBRARY_PATH=/tmp/native_client.tflite.Linux/:$LD_LIBRARY_PATH

## Install asticoqui
### Install dependencies

Run the following command:

    $ go get -u github.com/asticode/go-asticoqui/...

### Install executables

Run the following command:

    $ go install github.com/asticode/go-asticoqui/cmd
    
# Example       
## Get the pre-trained model and scorer

Go to [this page](https://coqui.ai/english/coqui/v1.0.0-large-vocab) and click `Enter Email to Download` at the bottom of the page
    
## Get the audio files

Run the following commands: 

    $ cd /tmp/deepspeech
    $ wget https://github.com/coqui-ai/STT/releases/download/v1.0.0/audio-1.0.0.tar.gz
    $ tar xvfz audio-1.0.0.tar.gz
    
## Use this client

Run the following commands:

    $ go run coqui/main.go -model stt-1.0.0-model.tflite -scorer stt-1.0.0-model.scorer -audio audio/2830-3980-0043.wav
    
        Text: experience proves this
    
    $ go run coqui/main.go -model stt-1.0.0-model.tflite -scorer stt-1.0.0-model.scorer -audio audio/4507-16021-0012.wav
    
        Text: why should one hall on the way
        
    $ go run coqui/main.go -model stt-1.0.0-model.tflite -scorer stt-1.0.0-model.scorer -audio audio/8455-210777-0068.wav
    
        Text: your power is sufficient i said