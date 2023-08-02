# Summary

 Members                        | Descriptions                                
--------------------------------|---------------------------------------------
`class `[`Camera`](#class_camera) | The main class for controlling a camera using the provided [ImageSensor](#class_image_sensor).
`class `[`FrameBuffer`](#class_frame_buffer) | Frame buffer class for storing captured frames.
`class `[`ImageSensor`](#class_image_sensor) | Abstract base class for image sensor drivers.
`class `[`ScanResults`](#class_scan_results) | A template class used to store the results from an I2C scan.

# class `Camera` {#class_camera}

The main class for controlling a camera using the provided [ImageSensor](#class_image_sensor).

## Summary

 Members                        | Descriptions                                
--------------------------------|---------------------------------------------
`public  `[`Camera`](#class_camera_1ab2978e9cd3c09af9b57df3844d92d1ed)`(`[`ImageSensor`](#class_image_sensor)` & sensor)` | Pointer to the frame buffer.
`public bool `[`begin`](#class_camera_1aa3985bb1568ada232901a8913aa3fe67)`(int32_t resolution,int32_t pixformat,int32_t framerate)` | Initialize the camera.
`public int `[`getID`](#class_camera_1aecf6d302d91984de1c5f66b5dc4fb126)`()` | Get the I2C address of the image sensor.
`public int `[`setFrameRate`](#class_camera_1a517e263c49fcb410862624e0fe2c10df)`(int32_t framerate)` | Set the frame rate of the image sensor.
`public int `[`setResolution`](#class_camera_1ab0018c1d6bb156075bfd331e6c07b75d)`(int32_t resolution)` | Set the resolution of the image sensor.
`public int `[`setPixelFormat`](#class_camera_1ab4eb6ed9f5f9a7b07b0e5b00c231c88f)`(int32_t pixelformat)` | Set the pixel (color) format of the image sensor.
`public int `[`setStandby`](#class_camera_1a8b1c93067e28f2a31589fcb8f9838c47)`(bool enable)` | Set the sensor in standby mode.
`public int `[`setTestPattern`](#class_camera_1aecbbed4890bf02d9fe4b0721f313ea35)`(bool enable,bool walking)` | Set the test pattern mode for the sensor.
`public int `[`frameSize`](#class_camera_1aee2784050787c5f081136023162bf2db)`()` | Get the frame size. This is the number of bytes in a frame as determined by the resolution and pixel format.
`public int `[`grabFrame`](#class_camera_1a5c7a0168ff7f69c07387702f02d4dfc8)`(`[`FrameBuffer`](#class_frame_buffer)` & fb,uint32_t timeout)` | Capture a frame.
`public int `[`enableMotionDetection`](#class_camera_1a784dd3f226d4491cf3a4525240e1bbc4)`(`[`md_callback_t`](#camera_8h_1a7b125b081eaf34de0aed22e32dd18587)` callback)` | Enable motion detection with the specified callback.
`public int `[`disableMotionDetection`](#class_camera_1a9bd4a1ce54df809ad6e92d91c640af1c)`()` | Disable motion detection.
`public int `[`setMotionDetectionWindow`](#class_camera_1a680ecb10f9b0a4dbac1ba7e8fa13b32f)`(uint32_t x,uint32_t y,uint32_t w,uint32_t h)` | Set the motion detection window.
`public int `[`setMotionDetectionThreshold`](#class_camera_1aaf4ec93c2facf50e37abadd1d2bc963a)`(uint32_t threshold)` | Set the motion detection threshold. On the Himax HM01B0, the recommended threshold range is 3 - 240 (0x03 to 0xF0).
`public int `[`motionDetected`](#class_camera_1ad120d322ec4ad36af100352b8e5a8620)`()` | Check if motion was detected and clear the motion detection flag.
`public void `[`debug`](#class_camera_1a4477c31738248824b47844a796aecb55)`(Stream & stream)` | Output debug information to a stream. You can use this function to output debug information to the serial port by passing Serial as the stream.

## Members

#### `public  `[`Camera`](#class_camera_1ab2978e9cd3c09af9b57df3844d92d1ed)`(`[`ImageSensor`](#class_image_sensor)` & sensor)` {#class_camera_1ab2978e9cd3c09af9b57df3844d92d1ed}

Pointer to the frame buffer.

Construct a new [Camera](#class_camera) object.

#### Parameters
* `sensor` Reference to the [ImageSensor](#class_image_sensor) object that is the driver for the camera sensor.

#### `public bool `[`begin`](#class_camera_1aa3985bb1568ada232901a8913aa3fe67)`(int32_t resolution,int32_t pixformat,int32_t framerate)` {#class_camera_1aa3985bb1568ada232901a8913aa3fe67}

Initialize the camera.

#### Parameters
* `resolution` Initial resolution (default: CAMERA_R320x240). Note that not all resolutions are supported by all cameras. 

* `pixformat` Initial pixel format (default: CAMERA_GRAYSCALE). Note that not all pixel formats are supported by all cameras. 

* `framerate` Initial frame rate (default: 30) 

#### Returns
true If the camera is successfully initialized 

#### Returns
false Otherwise

#### `public int `[`getID`](#class_camera_1aecf6d302d91984de1c5f66b5dc4fb126)`()` {#class_camera_1aecf6d302d91984de1c5f66b5dc4fb126}

Get the I2C address of the image sensor.

#### Returns
int The sensor ID

#### `public int `[`setFrameRate`](#class_camera_1a517e263c49fcb410862624e0fe2c10df)`(int32_t framerate)` {#class_camera_1a517e263c49fcb410862624e0fe2c10df}

Set the frame rate of the image sensor.

This has no effect on cameras that do not support variable frame rates. 

#### Parameters
* `framerate` The desired frame rate in frames per second 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`setResolution`](#class_camera_1ab0018c1d6bb156075bfd331e6c07b75d)`(int32_t resolution)` {#class_camera_1ab0018c1d6bb156075bfd331e6c07b75d}

Set the resolution of the image sensor.

This has no effect on cameras that do not support variable resolutions. 

#### Parameters
* `resolution` The desired resolution, as defined in the resolution enum 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`setPixelFormat`](#class_camera_1ab4eb6ed9f5f9a7b07b0e5b00c231c88f)`(int32_t pixelformat)` {#class_camera_1ab4eb6ed9f5f9a7b07b0e5b00c231c88f}

Set the pixel (color) format of the image sensor.

This has no effect on cameras that do not support variable pixel formats. e.g. the Himax HM01B0 only supports grayscale. 

#### Parameters
* `pixelformat` The desired pixel format, as defined in the pixel format enum 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`setStandby`](#class_camera_1a8b1c93067e28f2a31589fcb8f9838c47)`(bool enable)` {#class_camera_1a8b1c93067e28f2a31589fcb8f9838c47}

Set the sensor in standby mode.

This has no effect on cameras that do not support standby mode. 

#### Parameters
* `enable` true to enable standby mode, false to disable 

#### Returns
int 0 on success, non-zero on failure (or not implemented)

#### `public int `[`setTestPattern`](#class_camera_1aecbbed4890bf02d9fe4b0721f313ea35)`(bool enable,bool walking)` {#class_camera_1aecbbed4890bf02d9fe4b0721f313ea35}

Set the test pattern mode for the sensor.

#### Parameters
* `enable` true to enable test pattern, false to disable 

* `walking` true for walking test pattern, false for other test pattern (if supported) The walking test pattern alternates between black and white pixels which is useful for detecting stuck-at faults 

#### Returns
int 0 on success, non-zero on failure (or not implemented)

#### `public int `[`frameSize`](#class_camera_1aee2784050787c5f081136023162bf2db)`()` {#class_camera_1aee2784050787c5f081136023162bf2db}

Get the frame size. This is the number of bytes in a frame as determined by the resolution and pixel format.

#### Returns
int The frame size in bytes

#### `public int `[`grabFrame`](#class_camera_1a5c7a0168ff7f69c07387702f02d4dfc8)`(`[`FrameBuffer`](#class_frame_buffer)` & fb,uint32_t timeout)` {#class_camera_1a5c7a0168ff7f69c07387702f02d4dfc8}

Capture a frame.

#### Parameters
* `fb` Reference to a [FrameBuffer](#class_frame_buffer) object to store the frame data 

* `timeout` Time in milliseconds to wait for a frame (default: 5000) 

#### Returns
int 0 if successful, non-zero otherwise

#### `public int `[`enableMotionDetection`](#class_camera_1a784dd3f226d4491cf3a4525240e1bbc4)`(`[`md_callback_t`](#camera_8h_1a7b125b081eaf34de0aed22e32dd18587)` callback)` {#class_camera_1a784dd3f226d4491cf3a4525240e1bbc4}

Enable motion detection with the specified callback.

This has no effect on cameras that do not support motion detection. 

#### Parameters
* `callback` Function to be called when motion is detected 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`disableMotionDetection`](#class_camera_1a9bd4a1ce54df809ad6e92d91c640af1c)`()` {#class_camera_1a9bd4a1ce54df809ad6e92d91c640af1c}

Disable motion detection.

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`setMotionDetectionWindow`](#class_camera_1a680ecb10f9b0a4dbac1ba7e8fa13b32f)`(uint32_t x,uint32_t y,uint32_t w,uint32_t h)` {#class_camera_1a680ecb10f9b0a4dbac1ba7e8fa13b32f}

Set the motion detection window.

#### Parameters
* `x` The x-coordinate of the window origin 

* `y` The y-coordinate of the window origin 

* `w` The width of the window 

* `h` The height of the window 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`setMotionDetectionThreshold`](#class_camera_1aaf4ec93c2facf50e37abadd1d2bc963a)`(uint32_t threshold)` {#class_camera_1aaf4ec93c2facf50e37abadd1d2bc963a}

Set the motion detection threshold. On the Himax HM01B0, the recommended threshold range is 3 - 240 (0x03 to 0xF0).

#### Parameters
* `threshold` The motion detection threshold 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`motionDetected`](#class_camera_1ad120d322ec4ad36af100352b8e5a8620)`()` {#class_camera_1ad120d322ec4ad36af100352b8e5a8620}

Check if motion was detected and clear the motion detection flag.

This function must be called after the motion detection callback was executed to clear the motion detection flag. 

#### Returns
int 0 if no motion is detected, non-zero if motion is detected

#### `public void `[`debug`](#class_camera_1a4477c31738248824b47844a796aecb55)`(Stream & stream)` {#class_camera_1a4477c31738248824b47844a796aecb55}

Output debug information to a stream. You can use this function to output debug information to the serial port by passing Serial as the stream.

#### Parameters
* `stream` Stream to output the debug information

# class `FrameBuffer` {#class_frame_buffer}

Frame buffer class for storing captured frames.

## Summary

 Members                        | Descriptions                                
--------------------------------|---------------------------------------------
`public  `[`FrameBuffer`](#class_frame_buffer_1a2b9881f76922681e3295f848373e2e1a)`(int32_t x,int32_t y,int32_t bpp)` | Flag indicating if the buffer is allocated on the heap.
`public  `[`FrameBuffer`](#class_frame_buffer_1a022e61048a47fee8c4fc9983ac235466)`(int32_t address)` | Construct a new [FrameBuffer](#class_frame_buffer) object with a given address. This is useful if a resolution higher than 320x240 is required and external RAM shall be used. In thast case, the following code can be used:
`public  `[`FrameBuffer`](#class_frame_buffer_1a6f3763f4551f221b86ca033e2b315c42)`()` | Construct a new [FrameBuffer](#class_frame_buffer) object with no custom size or address.
`public uint32_t `[`getBufferSize`](#class_frame_buffer_1aa2101841a783e6a26b0ca95664b98bac)`()` | Get the buffer size in bytes.
`public uint8_t * `[`getBuffer`](#class_frame_buffer_1a828f6daea1f7a4f8ba895554b9880ea4)`()` | Get a pointer to the frame buffer. This can be used to read the pixels from the frame buffer. E.g. to print all pixels to the serial monitor as hex values:
`public void `[`setBuffer`](#class_frame_buffer_1aad534a8fa43ac21d42487392ab308b9e)`(uint8_t * buffer)` | Set the frame buffer pointer.
`public bool `[`hasFixedSize`](#class_frame_buffer_1a589deca39673dee89916488f49869da3)`()` | Check if the frame buffer has a fixed size. This is the case if the frame buffer is constructed with a width, height, and bits per pixel.
`public bool `[`isAllocated`](#class_frame_buffer_1ac6393d860fd75136451f75b9e1a71336)`()` | Check if the frame buffer is allocated on the heap.

## Members

#### `public  `[`FrameBuffer`](#class_frame_buffer_1a2b9881f76922681e3295f848373e2e1a)`(int32_t x,int32_t y,int32_t bpp)` {#class_frame_buffer_1a2b9881f76922681e3295f848373e2e1a}

Flag indicating if the buffer is allocated on the heap.

Construct a new [FrameBuffer](#class_frame_buffer) object with a fixed size.

#### Parameters
* `x` Width of the frame buffer 

* `y` Height of the frame buffer 

* `bpp` Bits per pixel

#### `public  `[`FrameBuffer`](#class_frame_buffer_1a022e61048a47fee8c4fc9983ac235466)`(int32_t address)` {#class_frame_buffer_1a022e61048a47fee8c4fc9983ac235466}

Construct a new [FrameBuffer](#class_frame_buffer) object with a given address. This is useful if a resolution higher than 320x240 is required and external RAM shall be used. In thast case, the following code can be used:

```cpp
#include "SDRAM.h"
[FrameBuffer](#class_frame_buffer) fb(SDRAM_START_ADDRESS);
...
// In setup() add:
SDRAM.begin();
```

#### Parameters
* `address` The memory address of the frame buffer

#### `public  `[`FrameBuffer`](#class_frame_buffer_1a6f3763f4551f221b86ca033e2b315c42)`()` {#class_frame_buffer_1a6f3763f4551f221b86ca033e2b315c42}

Construct a new [FrameBuffer](#class_frame_buffer) object with no custom size or address.

#### `public uint32_t `[`getBufferSize`](#class_frame_buffer_1aa2101841a783e6a26b0ca95664b98bac)`()` {#class_frame_buffer_1aa2101841a783e6a26b0ca95664b98bac}

Get the buffer size in bytes.

#### Returns
uint32_t The buffer size in bytes

#### `public uint8_t * `[`getBuffer`](#class_frame_buffer_1a828f6daea1f7a4f8ba895554b9880ea4)`()` {#class_frame_buffer_1a828f6daea1f7a4f8ba895554b9880ea4}

Get a pointer to the frame buffer. This can be used to read the pixels from the frame buffer. E.g. to print all pixels to the serial monitor as hex values:

```cpp
uint8_t *fb = fb.getBuffer();
for (int i = 0; i < fb.getBufferSize(); i++) {
   Serial.print(fb[i], HEX);
  Serial.print(" ");
}
```

#### Returns
uint8_t* Pointer to the frame buffer

#### `public void `[`setBuffer`](#class_frame_buffer_1aad534a8fa43ac21d42487392ab308b9e)`(uint8_t * buffer)` {#class_frame_buffer_1aad534a8fa43ac21d42487392ab308b9e}

Set the frame buffer pointer.

#### Parameters
* `buffer` Pointer to the frame buffer

#### `public bool `[`hasFixedSize`](#class_frame_buffer_1a589deca39673dee89916488f49869da3)`()` {#class_frame_buffer_1a589deca39673dee89916488f49869da3}

Check if the frame buffer has a fixed size. This is the case if the frame buffer is constructed with a width, height, and bits per pixel.

#### Returns
true If the frame buffer has a fixed size 

#### Returns
false Otherwise

#### `public bool `[`isAllocated`](#class_frame_buffer_1ac6393d860fd75136451f75b9e1a71336)`()` {#class_frame_buffer_1ac6393d860fd75136451f75b9e1a71336}

Check if the frame buffer is allocated on the heap.

#### Returns
true If the frame buffer is allocated 

#### Returns
false Otherwise

# class `ImageSensor` {#class_image_sensor}

Abstract base class for image sensor drivers.

## Summary

 Members                        | Descriptions                                
--------------------------------|---------------------------------------------
`public inline virtual  `[`~ImageSensor`](#class_image_sensor_1a39dd3d503eeae8d8397693f4117f386d)`()` | 
`public int `[`init`](#class_image_sensor_1afcd75040decc98a873555784c7d720f4)`()` | Initialize the image sensor. This prepares the sensor for capturing frames by setting the registers to their default values.
`public int `[`reset`](#class_image_sensor_1a7d1160e5f03f60a228d62f47c34bdc0f)`()` | Reset the image sensor. This is useful if the sensor is stuck.
`public int `[`getID`](#class_image_sensor_1af784a1a10367315b956f8a1311d5592b)`()` | Get the I2C address of the image sensor.
`public bool `[`getMono`](#class_image_sensor_1af58e03556bfdcaaa2767e6a63518ddb5)`()` | Check if the image sensor is monochrome aka grayscale.
`public uint32_t `[`getClockFrequency`](#class_image_sensor_1ad3ecadc277e3eba7e10126ff428a3cf9)`()` | Get the clock frequency of the image sensor.
`public int `[`setFrameRate`](#class_image_sensor_1a7bf22b279f789a8c6a0a98d74f4f5ee1)`(int32_t framerate)` | Set the frame rate of the image sensor.
`public int `[`setResolution`](#class_image_sensor_1a5a268c7d4be89fc8b44f615327d9e4a1)`(int32_t resolution)` | Set the resolution of the image sensor.
`public int `[`setPixelFormat`](#class_image_sensor_1a2d38e9237cb4d4c6063ae5111a8edb41)`(int32_t pixelformat)` | Set the pixel (color) format of the image sensor.
`public int `[`enableMotionDetection`](#class_image_sensor_1ab6bee7094526040aee4fd096166732b0)`(`[`md_callback_t`](#camera_8h_1a7b125b081eaf34de0aed22e32dd18587)` callback)` | Enable motion detection with the specified callback.
`public int `[`disableMotionDetection`](#class_image_sensor_1ab5c1fc3e85b37cc2eb3c5dfca988f421)`()` | Disable motion detection.
`public int `[`setMotionDetectionWindow`](#class_image_sensor_1ab1820a5189cb7f62c936b0e9dc9dff85)`(uint32_t x,uint32_t y,uint32_t w,uint32_t h)` | Set the motion detection window.
`public int `[`setMotionDetectionThreshold`](#class_image_sensor_1a3ae6e213cbc035deb025345d338446ce)`(uint32_t threshold)` | Set the motion detection threshold. On the Himax HM01B0, the recommended threshold range is 3 - 240 (0x03 to 0xF0).
`public int `[`motionDetected`](#class_image_sensor_1a5edcebecbc5c0747417c780905ff6a5f)`()` | Check if motion was detected and clear the motion detection flag.
`public void `[`debug`](#class_image_sensor_1a0d61c4c4d010721e178115a9535b3e89)`(Stream & stream)` | Output debug information to a stream. You can use this function to output debug information to the serial port by passing Serial as the stream.
`public inline virtual int `[`setStandby`](#class_image_sensor_1a6959dcdf86458c60d17efa26d63236e4)`(bool enable)` | Set the sensor in standby mode.
`public inline virtual int `[`setTestPattern`](#class_image_sensor_1a397e568f54cdf2c85d6c1124ed500335)`(bool enable,bool walking)` | Set the test pattern mode for the sensor.

## Members

#### `public inline virtual  `[`~ImageSensor`](#class_image_sensor_1a39dd3d503eeae8d8397693f4117f386d)`()` {#class_image_sensor_1a39dd3d503eeae8d8397693f4117f386d}

#### `public int `[`init`](#class_image_sensor_1afcd75040decc98a873555784c7d720f4)`()` {#class_image_sensor_1afcd75040decc98a873555784c7d720f4}

Initialize the image sensor. This prepares the sensor for capturing frames by setting the registers to their default values.

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`reset`](#class_image_sensor_1a7d1160e5f03f60a228d62f47c34bdc0f)`()` {#class_image_sensor_1a7d1160e5f03f60a228d62f47c34bdc0f}

Reset the image sensor. This is useful if the sensor is stuck.

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`getID`](#class_image_sensor_1af784a1a10367315b956f8a1311d5592b)`()` {#class_image_sensor_1af784a1a10367315b956f8a1311d5592b}

Get the I2C address of the image sensor.

#### Returns
int The sensor ID

#### `public bool `[`getMono`](#class_image_sensor_1af58e03556bfdcaaa2767e6a63518ddb5)`()` {#class_image_sensor_1af58e03556bfdcaaa2767e6a63518ddb5}

Check if the image sensor is monochrome aka grayscale.

#### Returns
true If the sensor is monochrome 

#### Returns
false Otherwise

#### `public uint32_t `[`getClockFrequency`](#class_image_sensor_1ad3ecadc277e3eba7e10126ff428a3cf9)`()` {#class_image_sensor_1ad3ecadc277e3eba7e10126ff428a3cf9}

Get the clock frequency of the image sensor.

#### Returns
uint32_t The clock frequency in Hz

#### `public int `[`setFrameRate`](#class_image_sensor_1a7bf22b279f789a8c6a0a98d74f4f5ee1)`(int32_t framerate)` {#class_image_sensor_1a7bf22b279f789a8c6a0a98d74f4f5ee1}

Set the frame rate of the image sensor.

This has no effect on cameras that do not support variable frame rates. 

#### Parameters
* `framerate` The desired frame rate in frames per second 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`setResolution`](#class_image_sensor_1a5a268c7d4be89fc8b44f615327d9e4a1)`(int32_t resolution)` {#class_image_sensor_1a5a268c7d4be89fc8b44f615327d9e4a1}

Set the resolution of the image sensor.

This has no effect on cameras that do not support variable resolutions. 

#### Parameters
* `resolution` The desired resolution, as defined in the resolution enum 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`setPixelFormat`](#class_image_sensor_1a2d38e9237cb4d4c6063ae5111a8edb41)`(int32_t pixelformat)` {#class_image_sensor_1a2d38e9237cb4d4c6063ae5111a8edb41}

Set the pixel (color) format of the image sensor.

This has no effect on cameras that do not support variable pixel formats. e.g. the Himax HM01B0 only supports grayscale. 

#### Parameters
* `pixelformat` The desired pixel format, as defined in the pixel format enum 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`enableMotionDetection`](#class_image_sensor_1ab6bee7094526040aee4fd096166732b0)`(`[`md_callback_t`](#camera_8h_1a7b125b081eaf34de0aed22e32dd18587)` callback)` {#class_image_sensor_1ab6bee7094526040aee4fd096166732b0}

Enable motion detection with the specified callback.

This has no effect on cameras that do not support motion detection. 

#### Parameters
* `callback` Function to be called when motion is detected 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`disableMotionDetection`](#class_image_sensor_1ab5c1fc3e85b37cc2eb3c5dfca988f421)`()` {#class_image_sensor_1ab5c1fc3e85b37cc2eb3c5dfca988f421}

Disable motion detection.

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`setMotionDetectionWindow`](#class_image_sensor_1ab1820a5189cb7f62c936b0e9dc9dff85)`(uint32_t x,uint32_t y,uint32_t w,uint32_t h)` {#class_image_sensor_1ab1820a5189cb7f62c936b0e9dc9dff85}

Set the motion detection window.

#### Parameters
* `x` The x-coordinate of the window origin 

* `y` The y-coordinate of the window origin 

* `w` The width of the window 

* `h` The height of the window 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`setMotionDetectionThreshold`](#class_image_sensor_1a3ae6e213cbc035deb025345d338446ce)`(uint32_t threshold)` {#class_image_sensor_1a3ae6e213cbc035deb025345d338446ce}

Set the motion detection threshold. On the Himax HM01B0, the recommended threshold range is 3 - 240 (0x03 to 0xF0).

#### Parameters
* `threshold` The motion detection threshold 

#### Returns
int 0 on success, non-zero on failure

#### `public int `[`motionDetected`](#class_image_sensor_1a5edcebecbc5c0747417c780905ff6a5f)`()` {#class_image_sensor_1a5edcebecbc5c0747417c780905ff6a5f}

Check if motion was detected and clear the motion detection flag.

This function must be called after the motion detection callback was executed to clear the motion detection flag. 

#### Returns
int 0 if no motion is detected, non-zero if motion is detected

#### `public void `[`debug`](#class_image_sensor_1a0d61c4c4d010721e178115a9535b3e89)`(Stream & stream)` {#class_image_sensor_1a0d61c4c4d010721e178115a9535b3e89}

Output debug information to a stream. You can use this function to output debug information to the serial port by passing Serial as the stream.

#### Parameters
* `stream` Stream to output the debug information

#### `public inline virtual int `[`setStandby`](#class_image_sensor_1a6959dcdf86458c60d17efa26d63236e4)`(bool enable)` {#class_image_sensor_1a6959dcdf86458c60d17efa26d63236e4}

Set the sensor in standby mode.

This has no effect on cameras that do not support standby mode. 

#### Parameters
* `enable` true to enable standby mode, false to disable 

#### Returns
int 0 on success, non-zero on failure (or not implemented)

#### `public inline virtual int `[`setTestPattern`](#class_image_sensor_1a397e568f54cdf2c85d6c1124ed500335)`(bool enable,bool walking)` {#class_image_sensor_1a397e568f54cdf2c85d6c1124ed500335}

Set the test pattern mode for the sensor.

#### Parameters
* `enable` true to enable test pattern, false to disable 

* `walking` true for walking test pattern, false for other test pattern (if supported) The walking test pattern alternates between black and white pixels which is useful for detecting stuck-at faults 

#### Returns
int 0 on success, non-zero on failure (or not implemented)

# class `ScanResults` {#class_scan_results}

A template class used to store the results from an I2C scan.

#### Parameters
* `T` Data type for the device address (e.g. uint8_t)

## Summary

 Members                        | Descriptions                                
--------------------------------|---------------------------------------------
`public inline bool `[`operator==`](#class_scan_results_1a49a4d2a33f8067df8e3d565c3873c4ac)`(T toBeFound)` | Equality operator to check if a given device address is found in the [ScanResults](#class_scan_results).
`public inline bool `[`operator!=`](#class_scan_results_1ad6c2ea590ee6f93d3c15c7da8294a38d)`(T toBeFound)` | Inequality operator to check if a given device address is not found in the [ScanResults](#class_scan_results).
`public inline void `[`push`](#class_scan_results_1a69527ec15005c5569bb8cc24b32d6b40)`(T obj)` | Add a device address to the [ScanResults](#class_scan_results).

## Members

#### `public inline bool `[`operator==`](#class_scan_results_1a49a4d2a33f8067df8e3d565c3873c4ac)`(T toBeFound)` {#class_scan_results_1a49a4d2a33f8067df8e3d565c3873c4ac}

Equality operator to check if a given device address is found in the [ScanResults](#class_scan_results).

#### Parameters
* `toBeFound` The device address to be checked 

#### Returns
true If the device address is found in the [ScanResults](#class_scan_results)

#### Returns
false Otherwise

#### `public inline bool `[`operator!=`](#class_scan_results_1ad6c2ea590ee6f93d3c15c7da8294a38d)`(T toBeFound)` {#class_scan_results_1ad6c2ea590ee6f93d3c15c7da8294a38d}

Inequality operator to check if a given device address is not found in the [ScanResults](#class_scan_results).

#### Parameters
* `toBeFound` The device address to be checked 

#### Returns
true If the device address is not found in the [ScanResults](#class_scan_results)

#### Returns
false Otherwise

#### `public inline void `[`push`](#class_scan_results_1a69527ec15005c5569bb8cc24b32d6b40)`(T obj)` {#class_scan_results_1a69527ec15005c5569bb8cc24b32d6b40}

Add a device address to the [ScanResults](#class_scan_results).

#### Parameters
* `obj` The device address to be added

Generated by [Moxygen](https://sourcey.com/moxygen)