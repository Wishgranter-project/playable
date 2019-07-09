This package describes an universal API for multimedia players. It offers an interface ( as well a base class ) to write wrappers around different multimedia players, so they may be more easily interchanged.

See these implementations for example:

- [YouTube embbed api](https://github.com/adinan-cenci/js-youtube-wrapper)
- [Native audio/video tags](https://github.com/adinan-cenci/js-html-multimedia-wrapper)

## The interface

### Properties

| Property            |                                                              |
| ------------------- | ------------------------------------------------------------ |
| paused              | Boolean                                                      |
| playing             | Boolean                                                      |
| reproducing         | Boolean. A player may be in the state of playing <br />but not reproducing, it may be buffering and still not be paused. |
| buffering           | Boolean                                                      |
| waiting             | Boolean. When true it means that the player cannot start reproduction and is waiting to buffer enough content. |
| duration            | Float, seconds                                               |
| currentTime         | Float, seconds                                               |
| remainingTime       | Float, seconds                                               |
| durationTimer       | String, ISO 8601 formated as hh:mm:ss                        |
| currentTimer        | String, ISO 8601 formated as hh:mm:ss                        |
| remainingTimer      | String, ISO 8601 formated as hh:mm:ss                        |
| currentPercentage   | Float, 0 - 100                                               |
| remainingPercentage | Float, 0 - 100                                               |

### Methods

| Method                             |                                                              |
| ---------------------------------- | ------------------------------------------------------------ |
| contructor(settings)               | @Settings: May differ for each vendor                        |
| setData(data)                      | Returns a promise to resolve once the player is ready to reproduce. <br />@Data: Object describing the media to be played, it may differ for each vendor, but preferably use properties such as: "href", "src". |
| play(time = null)                  | Starts/resumes reproduction, will skip to a particular section if informed.<br />@Time: Accepts <br /> - a float <br /> - an ISO 8601 formated string hh:mm:ss <br /> - a numerical string suffixed with % |
| pause()                            |                                                              |
| setCurrentTime(time)               | @Time: Accepts <br /> - a float <br /> - an ISO 8601 formated string hh:mm:ss <br /> - a numerical string suffixed with % |
| seek(time)                         | Alias to setCurrentTime                                      |
| setVolume(vol)                     | @Vol: It accepts an integer between 0 and 100 <br /> Or a float between 0.00 and 1.00 for compatibility sake |
| getSeconds(perc, formated = false) | Returns the seconds corresponding to perc %. <br />@Perc: Float between 0 and 100 <br />@Formated: Bool, if true it will return an ISO 8601 formated as hh:mm:ss |
| getPercentage(time)                | Returns the percentage corresponding to time<br /> @Time: int, float, string, either a number or ISO 8601 formated string hh:mm:ss<br /> @Return float |

### Callbacks

| Callback        |                                                  |
| --------------- | ------------------------------------------------ |
| onError(error)  |                                                  |
| onEnded()       |                                                  |
| onTimeupdate()  | It is called as the reproduction progresses.     |
| onStateChange() | Paused, playing, reproducing, buffering, waiting |

