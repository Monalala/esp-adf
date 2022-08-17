Project Design
**************

:link_to_translation:`zh_CN:[中文]`

When designing a project with ability to process audio signals or audio data we typically consider a subset of the following components:

**Input:**

* **Analog signal input** is to connect equipment. (e.g. a microphone)
* **Storage media** is to read audio files. ( e.g. microSD card)
* **Wi-Fi interface** is to obtain an audio data stream from the internet.
* **Bluetooth interface** is to obtain an audio data stream from wquipment. (e.g. a Bluetooth headset)
* **I2S interface** is to obtain audio data stream from a codec chip.
* **Ethernet interface** is to obtain an audio data stream from the internet.
* An **internal chip's flash memory** is to play some audio samples.
* **User Interface** is to provide user input. (e.g. buttons or some other means)

**Output:**

* **Analog signal output** is to connect headphones or speakers.
* **Storage media** (e.g. microSD card) is to write some audio files through recording.
* **Wi-Fi interface** is to send out an audio data stream to the internet.
* **Bluetooth interface** is to stream audio data to equipment (e.g. a Bluetooth headset).
* **I2S interface** is to stream some data to a codec chip.
* **Ethernet interface** is to stream an audio data stream to the internet.
* An **internal chip's flash memory** is to store some audio recording.
* **User Interface** is about a display, LEDs or some means of `haptic <https://en.wikipedia.org/wiki/Haptic_technology>`_ feedback

**Main Processing Unit:**

A microcontroller or a computer with processing power to read the data from the input, process (e.g. encode / encode) and send to the output.


Project Options
===============

The ESP chips (including ESP32, ESP32-S2, ESP32-S3) have all the above features or are able to support them (e.g. can drive Ethernet PHY). Considering the ESP chip cost is low, and availability of ESP-ADF software development platform, we are able to develop an audio project with minimum additional components at very low price.

Depending on the application, required functionality and performance, we may consider two project groups.

* **Minimum** - having minimum additional components, assuming using on board I2S, or PDM interface as well as DAC, if no high qualify audio on the output is required.
* **Typical** - with an external codec chip and a power amplifier, for high quality output audio and multiple input / output options.

There may be several variation between the above projects, by adding or removing features/components. Below are a couple of examples.


Project Minimum
===============

With several peripherals on an ESP chip, I2S or PDM or DAC interfaces can be used to implement a minimum project. With the digital microphones, we could input voice signals and build a command voice control project minimum that could communicate with a cloud service.

.. figure:: ../../_static/audio-project-minimum-voice-service.jpg
    :alt: Audio Project Example - Send Voice Commands to Cloud Service
    :figclass: align-center

    Audio Project Example - Send Voice Commands to Cloud Service

With two on board DACs, if 8-bit width on the output is satisfactory, we may implement another project minimum - a device to play an internet connected radio.

.. figure:: ../../_static/audio-project-minimum-internet-radio.jpg
    :alt: Audio Project Example - Internet Connected Radio Player
    :figclass: align-center

    Audio Project Example - Internet Connected Radio Player


Typical Project
===============

When looking for better audio quality and more interfacing options we would use an external I2S codec to do all the analog input and output signal processing. The codec chip, depending on type, may provide additional functionality like audio input signal preamplifier, headphone output amplifier, multiple analog input and outputs, sound effects, etc. The `I2S <http://iot-bits.com/wp-content/uploads/2017/06/I2SBUS.pdf>`_ is considered as the industry standard for interfacing with audio codec chips, or in general for a high speed, continuous transfer of the audio data. To optimize performance of audio data processing, an additional memory may be required. For such cases, please consider using `ESP32-WROVER-E <https://www.espressif.com/sites/default/files/documentation/esp32-wrover-e_esp32-wrover-ie_datasheet_en.pdf>`_ that provides 8 MB PSRAM on a single module together with the ESP32 chip.

.. figure:: ../../_static/audio-project-typical-example.jpg
    :alt: Typical Audio Project Example
    :figclass: align-center

    Typical Audio Project Example

The ESP-ADF is designed primarily to support projects with a codec chip. The :doc:`ESP32 LyraT <dev-boards/get-started-esp32-lyrat>` board is an example of such a project. The software interfacing with the board is done by Audio HAL and a driver. The codec chip used on the ESP32 LyraT is `ES8388 <http://www.everest-semi.com/pdf/ES8388%20DS.pdf>`_. Boards with a different codec chip may be supported by providing a different driver.