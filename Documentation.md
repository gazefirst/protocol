# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [Eyetracker.proto](#Eyetracker-proto)
    - [CalibrationControl](#GazeFirst-CalibrationControl)
    - [CalibrationPointMessage](#GazeFirst-CalibrationPointMessage)
    - [CalibrationResult](#GazeFirst-CalibrationResult)
    - [CalibrationStatus](#GazeFirst-CalibrationStatus)
    - [Configuration](#GazeFirst-Configuration)
    - [DeviceInformation](#GazeFirst-DeviceInformation)
    - [DeviceSettings](#GazeFirst-DeviceSettings)
    - [GazeData](#GazeFirst-GazeData)
    - [GazeSubscription](#GazeFirst-GazeSubscription)
    - [NormedPoint2D](#GazeFirst-NormedPoint2D)
    - [Positioning](#GazeFirst-Positioning)
    - [ScreenSize](#GazeFirst-ScreenSize)
    - [Settings](#GazeFirst-Settings)
    - [UserSettings](#GazeFirst-UserSettings)
  
    - [CalibrationControl.CalibrationPoints](#GazeFirst-CalibrationControl-CalibrationPoints)
    - [CalibrationControl.Control](#GazeFirst-CalibrationControl-Control)
    - [CalibrationPointMessage.PointState](#GazeFirst-CalibrationPointMessage-PointState)
    - [CalibrationStatus.Status](#GazeFirst-CalibrationStatus-Status)
  
    - [Eyetracker](#GazeFirst-Eyetracker)
  
- [Scalar Value Types](#scalar-value-types)



<a name="Eyetracker-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## Eyetracker.proto



<a name="GazeFirst-CalibrationControl"></a>

### CalibrationControl
CalibrationControl message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| control | [CalibrationControl.Control](#GazeFirst-CalibrationControl-Control) |  | Control message |
| calibrationPoints | [CalibrationControl.CalibrationPoints](#GazeFirst-CalibrationControl-CalibrationPoints) |  | Number of calibration points |
| size | [ScreenSize](#GazeFirst-ScreenSize) |  | Screen size in mm |






<a name="GazeFirst-CalibrationPointMessage"></a>

### CalibrationPointMessage
Calibration Point message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| sequence | [int32](#int32) |  | Sequence number of calibration point, starting at 0 |
| position | [NormedPoint2D](#GazeFirst-NormedPoint2D) |  | Calibration point position on screen |
| state | [CalibrationPointMessage.PointState](#GazeFirst-CalibrationPointMessage-PointState) |  | Calibration point state |






<a name="GazeFirst-CalibrationResult"></a>

### CalibrationResult
CalibrationResult message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| overallPercentageRating | [int32](#int32) |  | Overall percentage rating ( 0 - 100) |
| percentageRatings | [int32](#int32) | repeated | list of ints with percentage ratings per point ( 0 - 100) |
| percentageRatingsLeft | [int32](#int32) | repeated | list of ints with percentage ratings per point on left eye ( 0 - 100) |
| percentageRatingsRight | [int32](#int32) | repeated | list of ints with percentage ratings per point on right eye ( 0 - 100) |






<a name="GazeFirst-CalibrationStatus"></a>

### CalibrationStatus
CalibrationStatus message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| status | [CalibrationStatus.Status](#GazeFirst-CalibrationStatus-Status) |  | Calibration status |
| calibrationPoint | [CalibrationPointMessage](#GazeFirst-CalibrationPointMessage) |  | Calibration point message |
| calibrationResult | [CalibrationResult](#GazeFirst-CalibrationResult) |  | Calibration result |






<a name="GazeFirst-Configuration"></a>

### Configuration
Configuration message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| empty | [google.protobuf.Empty](#google-protobuf-Empty) |  | Empty message |
| settings | [Settings](#GazeFirst-Settings) |  | Settings message |






<a name="GazeFirst-DeviceInformation"></a>

### DeviceInformation
DeviceInformation message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| serial | [int64](#int64) |  | Serial of device |
| version | [string](#string) |  | Firmware version string |
| hwConfig | [int32](#int32) |  | Configuration ID of hardware |
| machine | [string](#string) |  | Machine version string |






<a name="GazeFirst-DeviceSettings"></a>

### DeviceSettings
DeviceSettings message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| update | [bool](#bool) |  | Set to true if the settings should be updated |
| pauseNative | [bool](#bool) |  | If true, native device processing is paused (e.g. on HID / USB) |
| pauseAPIGaze | [bool](#bool) |  | If true, gaze processing (API wise) is paused |






<a name="GazeFirst-GazeData"></a>

### GazeData
GazeData message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| timestamp | [int64](#int64) |  | Timestamp of gaze data |
| gazePoint | [NormedPoint2D](#GazeFirst-NormedPoint2D) |  | Combined gaze point |
| leftEye | [NormedPoint2D](#GazeFirst-NormedPoint2D) |  | Left eye gaze point |
| rightEye | [NormedPoint2D](#GazeFirst-NormedPoint2D) |  | Right eye gaze point |
| fixation | [bool](#bool) |  | True if gaze is fixated |
| userPresent | [bool](#bool) |  | True if user is present (normally yes). Device will send false with empty data once till a user gets redetected. |
| leftEyeOpen | [bool](#bool) |  | True if left eye is open / false if closed or user is not present |
| rightEyeOpen | [bool](#bool) |  | True if right eye is open / false if closed or user is not present |






<a name="GazeFirst-GazeSubscription"></a>

### GazeSubscription
GazeSubscription message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| unfiltered | [bool](#bool) |  | If true, unfiltered gaze data will be streamed |






<a name="GazeFirst-NormedPoint2D"></a>

### NormedPoint2D
NormedPoint2D message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| x | [double](#double) |  | X coordinate (0 - 1d) |
| y | [double](#double) |  | Y coordinate (0 - 1d) |
| invalid | [bool](#bool) |  | True if this point is not valid |






<a name="GazeFirst-Positioning"></a>

### Positioning
Positioning message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| depthInMM | [double](#double) |  |  |
| leftEyePos | [NormedPoint2D](#GazeFirst-NormedPoint2D) |  |  |
| rightEyePos | [NormedPoint2D](#GazeFirst-NormedPoint2D) |  |  |






<a name="GazeFirst-ScreenSize"></a>

### ScreenSize
ScreenSize message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| width_mm | [double](#double) |  | Screen dimensions in mm |
| height_mm | [double](#double) |  | Screen dimensions in mm |






<a name="GazeFirst-Settings"></a>

### Settings
Settings message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| size | [ScreenSize](#GazeFirst-ScreenSize) |  | Screen size in mm |
| userSettings | [UserSettings](#GazeFirst-UserSettings) |  | User settings |
| deviceSettings | [DeviceSettings](#GazeFirst-DeviceSettings) |  | Device settings |






<a name="GazeFirst-UserSettings"></a>

### UserSettings
UserSettings message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| update | [bool](#bool) |  | Set to true if the settings should be updated |
| smoothing | [int32](#int32) |  | 1 to 10, 1 is less smoothing, 10 is max smoothing |
| leftEyeOnly | [bool](#bool) |  | If true, only left eye data is used |
| rightEyeOnly | [bool](#bool) |  | If true, only right eye data is used |





 


<a name="GazeFirst-CalibrationControl-CalibrationPoints"></a>

### CalibrationControl.CalibrationPoints
Calibration Points (count) enum

| Name | Number | Description |
| ---- | ------ | ----------- |
| NINE | 0 | Nine point is default and mostly best |
| ONE | 1 |  |
| FIVE | 2 |  |
| THIRTEEN | 3 | - Do not use yet - |
| ZERO | 4 | Zero basically resets to a default calibration (only use this if user can not focus calibration points) |



<a name="GazeFirst-CalibrationControl-Control"></a>

### CalibrationControl.Control
Control enum

| Name | Number | Description |
| ---- | ------ | ----------- |
| START | 0 | Signal that a calibration should start |
| STOP | 1 | Signal that a calibration should stop |



<a name="GazeFirst-CalibrationPointMessage-PointState"></a>

### CalibrationPointMessage.PointState


| Name | Number | Description |
| ---- | ------ | ----------- |
| SHOW | 0 | GUI should show the point |
| ANIMATE | 1 | GUI should animate the point |
| HIDE | 2 | GUI should hide the point |



<a name="GazeFirst-CalibrationStatus-Status"></a>

### CalibrationStatus.Status
Status enum

| Name | Number | Description |
| ---- | ------ | ----------- |
| STARTED | 0 | Started the calibration / currently running. Check calibrationPoint payload for point data and status of it. Stream is open and active. |
| FAILED | 1 | Calibration failed, will keep current calibration. Stream will close. |
| SUCCEEDED | 2 | Calibration was successfull. Check calibrationResult payload for result. Stream stays open for future features (improve points). Client should close it when done! |


 

 


<a name="GazeFirst-Eyetracker"></a>

### Eyetracker
Eyetracker service

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| Calibrate | [CalibrationControl](#GazeFirst-CalibrationControl) stream | [CalibrationStatus](#GazeFirst-CalibrationStatus) stream | Calibrate device for user. Client should close stream when done. |
| SubscribePositioning | [.google.protobuf.Empty](#google-protobuf-Empty) | [Positioning](#GazeFirst-Positioning) stream | Subscribe to positioning data. Client should close stream when done. |
| SubscribeGaze | [GazeSubscription](#GazeFirst-GazeSubscription) | [GazeData](#GazeFirst-GazeData) stream | Subscribe to gaze data. Client should close stream when done. |
| Configure | [Configuration](#GazeFirst-Configuration) | [Settings](#GazeFirst-Settings) | Configure the device. |
| GetDeviceInfo | [.google.protobuf.Empty](#google-protobuf-Empty) | [DeviceInformation](#GazeFirst-DeviceInformation) | Get device information. |

 



## Scalar Value Types

| .proto Type | Notes | C++ | Java | Python | Go | C# | PHP | Ruby |
| ----------- | ----- | --- | ---- | ------ | -- | -- | --- | ---- |
| <a name="double" /> double |  | double | double | float | float64 | double | float | Float |
| <a name="float" /> float |  | float | float | float | float32 | float | float | Float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum or Fixnum (as required) |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="bool" /> bool |  | bool | boolean | boolean | bool | bool | boolean | TrueClass/FalseClass |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode | string | string | string | String (UTF-8) |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str | []byte | ByteString | string | String (ASCII-8BIT) |

