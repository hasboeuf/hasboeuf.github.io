---
layout: post
title: GPIO as a REST API
date: 2019-05-14 00:30:06 +0100
author: Adrien Gavignet
categories: iot arduino
---

Tired to upload a sketch everytime you need to interact with a GPIO?
Then I got a sketch for you.

I'm currently making a robot which needs several components, one of them is a simple controller connected to Wifi.
At the begining I planned to communicate with it through RF433 but at the end I decided not to (should write a blog post about it).

Instead I am using an ESP8266 based on NodeMCU firmware, you can find this for [less than 2$](https://fr.aliexpress.com/item/V2-4M-4FLASH-NodeMcu-Lua-WIFI-Networking-development-board-Based-ESP8266/32647690484.html).

Like any board of that type, the ESP8266 exposes some GPIO and I wanted them to be controlled by a REST API.

[Here](https://github.com/hasboeuf/domiotic/blob/master/arduino/nodemcu/restforgpio/README.md) is the sketch doing it.

## What for

This sketch has two purposes:

* Use it as is, to interact with your board when working on it without having to compile and upload hundred times.
* Show a way to handle a REST API on that kind of board, the routing logic is really generic and could be adapted to many usecases.

## Use case example

Suppose you want to control an electrical relay in order to start you coffee machine while you're getting off your bed. Sooner or later you will need to control at least one GPIO, let's say the PIN 3. In this case, you only need to:

* `curl -X PUT <ip>/gpio/3/mode/output` (if PIN 3 is not in OUTPUT mode)
* `curl -X PUT <ip>/gpio/3/value/high`

After 5 minutes your coffee is ready.

* `curl -X PUT <ip>/gpio/3/value/low`

Obviously those calls would need to be integrated to a home automation system like [Jeedom](https://www.jeedom.com/site/en/) but you get the overall idea ;).

## Under the hood

The code is using a generic `Router` class which allows you to do things like this:

```c
router.addRoute(HTTP_METHOD, endpoint, callback);
```

* `HTTP_METHOD`: HTTP_GET, HTTP_PUT, etc.
* `endpoint`: Regular expression that defines your endpoint.
* `callback`: A callback which takes as a parameter a list of arguments, first argument is the URL of the request, followed by captured strings of your regular expression (if any).

In this example:

```c
void handleGpioListOne(std::vector<std::string> args) {
}

void setup() {
    // ...
    router.addRoute(HTTP_GET, "^/gpio/(%d+)$", handleGpioListOne)
}
```

`handleGpioListOne` will be called on `<ip>/gpio/3` request with:

* `args[0] = "<ip>/gpio/3"`
* `args[1] = "3"`

Note: I first implemented the routing logic in a recursive manner, don't do it. You will hit memory issues, in the best scenario your program will start acting funky.

## Dependencies

* [Regex lib](https://github.com/nickgammon/Regexp): to handle endpoint's regular expressions (`std::regex` is not ported in the Arduino world yet).
* [ArduinoJson lib](https://arduinojson.org/): to manipulate JSON content easily.
