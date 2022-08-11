# Ebyroid-TTS-protocol
**Ebyroid-TTS-protocol ( Ebyroid-protocol ) is standardizes-simples HTTP-API for generic applications use of TTS.**  
## About

By solving and absorption specific platform-related issues, enables connectivity with a heterogeneous servers in developing applications use of TTS, and enables scaling of servers that provide TTS functionality. 
For this reason, it is ideal for developing experimental applications centering on voice distribution of text chat.

## Typical implementation
### [Ebyroid](https://github.com/nanokina/ebyroid) - This protocol standard is based on this application. Ebyroid is the node addon for VOICEROID+ and VOICEROID2.

### [VOICEVOX-ebyroid-proxy](https://github.com/Ebycow/VOICEVOX-ebyroid-proxy) - This application proxies the HTTP API provided by [VOICEVOX CORE](https://github.com/VOICEVOX/voicevox_core).

## API specification ( 2022-8-11 Draft )

### `GET /api/v1/audiostream`

#### query parameters

|  id   |  type  | required | desc             | example                      |
| :---: | :----: | :------: | :--------------- | :--------------------------- |
| text  | string | **yes**  | TTS content      | `text=今日は%20はじめまして` |
| name  | string |    no    | Voice Address | `name=kiritan-chan`          |

#### response types

- `200 OK` => `application/octet-stream`
- `4xx` and `5xx` => `application/json`

#### extra response headers

|               id               |        value        | desc            |
| :----------------------------: | :-----------------: | :-------------- |
|    Ebyroid-PCM-Sample-Rate     | `22050\|44100\|48000` | Samples per sec |
|     Ebyroid-PCM-Bit-Depth      |        `16`         | Fixed to 16-bit |
| Ebyroid-PCM-Number-Of-Channels |        `1\|2`        | Mono or Stereo  |

Note that these headers will be sent only with `200 OK`.

#### response body

A byte stream of the [Linear PCM](http://soundfile.sapp.org/doc/WaveFormat/) data.\
**The stream doesn't contain file header bytes since this endpoint is rather for those who want to deal with raw audio data.**\
Use `GET /api/v1/audiofile` instead if you demand `.wav` file.

### `GET /api/v1/audiofile`

#### query parameters

|  id   |  type  | required | desc             | example                    |
| :---: | :----: | :------: | :--------------- | :------------------------- |
| text  | string | **yes**  | TTS content      | `text=今晩は%20さようなら` |
| name  | string |    no    | Voice Address | `name=akane-chan`          |

#### response types

- `200 OK` => `audio/wav`
- `4xx` and `5xx` => `application/json`

#### extra response headers

None.

#### response body

Complete data for a `.wav` file.

## License
MIT. See LICENSE.

## catgirl

![ebyroid](https://user-images.githubusercontent.com/24854132/76497659-c90dc080-647e-11ea-9249-33bcc8d74f64.png)

## sister project
[Hanako](https://www.github.com/Ebycow/hanako) - Discord TTS Bot for Wide-Use
