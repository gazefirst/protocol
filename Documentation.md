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
    - [HostSettings](#GazeFirst-HostSettings)
    - [NormedPoint2D](#GazeFirst-NormedPoint2D)
    - [Positioning](#GazeFirst-Positioning)
    - [RawFrame](#GazeFirst-RawFrame)
    - [ScreenSize](#GazeFirst-ScreenSize)
    - [Settings](#GazeFirst-Settings)
    - [StreamUsersRequest](#GazeFirst-StreamUsersRequest)
    - [User](#GazeFirst-User)
    - [UserProfileRequest](#GazeFirst-UserProfileRequest)
    - [UserProfileResponse](#GazeFirst-UserProfileResponse)
    - [UserSettings](#GazeFirst-UserSettings)
    - [UserStreamResponse](#GazeFirst-UserStreamResponse)
  
    - [CalibrationControl.CalibrationPoints](#GazeFirst-CalibrationControl-CalibrationPoints)
    - [CalibrationControl.Control](#GazeFirst-CalibrationControl-Control)
    - [CalibrationPointMessage.PointState](#GazeFirst-CalibrationPointMessage-PointState)
    - [CalibrationStatus.Status](#GazeFirst-CalibrationStatus-Status)
    - [DeviceSettings.Framerate](#GazeFirst-DeviceSettings-Framerate)
    - [UserProfileRequest.OperationType](#GazeFirst-UserProfileRequest-OperationType)
    - [UserProfileResponse.Status](#GazeFirst-UserProfileResponse-Status)
  
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
| multipoint | [bool](#bool) |  | If true, multiple points will be displayed at the same time - also fixationBased will be forced to true. If false, only one point will be displayed at a time. |
| fixationBased | [bool](#bool) |  | If true, calibration is fixation based: |
| pointsToImprove | [int32](#int32) | repeated | on fixation detection (near or at target) state will be changed to ANIMATE, on fixation loss state will be changed to SHOW, after a certain amount of time / enough samples state will be changed to HIDE

List of points (their sequence number) that should be recalibrated / improved |
| manualCalibration | [bool](#bool) |  | Manual calibration: client needs to confirm every point by sending Control.CONFIRM - multipoint and fixationBased will be ignored |
| timestamp | [int64](#int64) |  | Timestamp (unix time) of calibration - set to starting time when sending START |






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
| canImprove | [bool](#bool) |  | Signals if the calibration can be improved (if false do not send Control.Improve!) |
| uid | [bytes](#bytes) |  | Unique ID of this calibration and its result - fixed to 16 bytes length |
| timestamp | [int64](#int64) |  | Timestamp (unix time) of calibration |






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
| cpuTemp | [double](#double) |  | CPU core temp in °C |






<a name="GazeFirst-DeviceSettings"></a>

### DeviceSettings
DeviceSettings message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| update | [bool](#bool) |  | Set to true if the settings should be updated |
| pauseNative | [bool](#bool) |  | If true, native device processing is paused (e.g. on HID / USB) |
| pauseAPIGaze | [bool](#bool) |  | If true, gaze processing (API wise) is paused |
| enablePauseByGaze | [bool](#bool) |  | If true, eyetracker native gaze data will be paused by looking into the eyetracker camera (center of screen) |
| framerate | [DeviceSettings.Framerate](#GazeFirst-DeviceSettings-Framerate) |  | Configure framerate |






<a name="GazeFirst-GazeData"></a>

### GazeData
GazeData message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| timestamp | [int64](#int64) |  | Timestamp (internal device time) of gaze data |
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






<a name="GazeFirst-HostSettings"></a>

### HostSettings
HostSettings message
Note: only for customized platform-dependent functions - these values do not have to be set.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| update | [bool](#bool) |  | Set to true if the settings should be updated |
| model | [string](#string) |  | Model |
| manufacturer | [string](#string) |  | Manufacturer |
| platform | [string](#string) |  | Platform |






<a name="GazeFirst-NormedPoint2D"></a>

### NormedPoint2D
NormedPoint2D message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| x | [double](#double) |  | X coordinate (0 - 1d) |
| y | [double](#double) |  | Y coordinate (0 - 1d) |
| invalid | [bool](#bool) |  | True if this point is not valid |
| hasConfidence | [bool](#bool) |  | True, if this point has a confidence value |
| confidence | [double](#double) |  | Confidence (0 - 1d) |






<a name="GazeFirst-Positioning"></a>

### Positioning
Positioning message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| depthInMM | [double](#double) |  | Distance in mm: Values usually range from 450mm to 800mm (45cm to 80cm). User distance from 550mm to 650mm is perfect, 500mm to 550mm and 650mm to 700mm are acceptable. |
| leftEyePos | [NormedPoint2D](#GazeFirst-NormedPoint2D) |  | Left eye position |
| rightEyePos | [NormedPoint2D](#GazeFirst-NormedPoint2D) |  | Right eye position |
| leftEyeClosed | [bool](#bool) |  | True if left eye is closed / false if open |
| rightEyeClosed | [bool](#bool) |  | True if right eye is closed / false if open |
| gazeIsPaused | [bool](#bool) |  | True if gaze is paused (user needs to look into the eyetracker camera to unpause) |






<a name="GazeFirst-RawFrame"></a>

### RawFrame
RawFrame message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| width | [int32](#int32) |  | Frame width |
| height | [int32](#int32) |  | Frame height |
| channels | [int32](#int32) |  | Number of channels |
| data | [bytes](#bytes) |  | Data as bytes (size = width * height * channels) |
| timestamp | [int64](#int64) |  | Timestamp (internal device time) of frame capture |






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
| hostSettings | [HostSettings](#GazeFirst-HostSettings) |  | Host settings |






<a name="GazeFirst-StreamUsersRequest"></a>

### StreamUsersRequest
Request message for streaming user profiles


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| stayOpen | [bool](#bool) |  | If true, the stream stays open to inform about changes. |






<a name="GazeFirst-User"></a>

### User
Message representing a user profile


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| userID | [int32](#int32) |  | Automatically generated identifier. |
| username | [string](#string) |  | User&#39;s chosen username. |
| uid | [bytes](#bytes) |  | Unique ID of this user, also device specific - fixed to 16 bytes length |






<a name="GazeFirst-UserProfileRequest"></a>

### UserProfileRequest
Request message for managing user profiles


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| operation | [UserProfileRequest.OperationType](#GazeFirst-UserProfileRequest-OperationType) |  | The type of operation to perform |
| userID | [int32](#int32) |  | Unique identifier for the user |
| username | [string](#string) |  | Username for CREATE and UPDATE operations. |






<a name="GazeFirst-UserProfileResponse"></a>

### UserProfileResponse
Response message including the status and information about the user.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| status | [UserProfileResponse.Status](#GazeFirst-UserProfileResponse-Status) |  | Status of the operation. |
| user | [User](#GazeFirst-User) |  | User profile information, included for CREATE, UPDATE and SELECT. |






<a name="GazeFirst-UserSettings"></a>

### UserSettings
UserSettings message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| update | [bool](#bool) |  | Set to true if the settings should be updated |
| smoothing | [int32](#int32) |  | 1 to 10, 1 is less smoothing, 10 is max smoothing |
| leftEyeOnly | [bool](#bool) |  | If true, only left eye data is used |
| rightEyeOnly | [bool](#bool) |  | If true, only right eye data is used |






<a name="GazeFirst-UserStreamResponse"></a>

### UserStreamResponse
Message for user stream responses


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| user | [User](#GazeFirst-User) |  | User profile information. |
| isActive | [bool](#bool) |  | Indicates if this is the currently active user. |





 


<a name="GazeFirst-CalibrationControl-CalibrationPoints"></a>

### CalibrationControl.CalibrationPoints
Calibration Points (count) enum

| Name | Number | Description |
| ---- | ------ | ----------- |
| NINE | 0 | Nine point is default and mostly best |
| ONE | 1 |  |
| FIVE | 2 |  |
| THIRTEEN | 3 |  |
| ZERO | 4 | Zero basically resets to a default calibration (only use this if user can not focus calibration points) |



<a name="GazeFirst-CalibrationControl-Control"></a>

### CalibrationControl.Control
Control enum

| Name | Number | Description |
| ---- | ------ | ----------- |
| START | 0 | Signal that a calibration should start |
| STOP | 1 | Signal that a calibration should stop |
| IMPROVE | 3 | Improve given points (pointsToImprove) |
| CONFIRM | 4 | Confirm last point (only valid when manualCalibration = true) |



<a name="GazeFirst-CalibrationPointMessage-PointState"></a>

### CalibrationPointMessage.PointState


| Name | Number | Description |
| ---- | ------ | ----------- |
| SHOW | 0 | GUI should show the point |
| ANIMATE | 1 | GUI should animate the point (eye tracker samples calibration data in this state only) |
| HIDE | 2 | GUI should hide the point |



<a name="GazeFirst-CalibrationStatus-Status"></a>

### CalibrationStatus.Status
Status enum

| Name | Number | Description |
| ---- | ------ | ----------- |
| STARTED | 0 | Started the calibration / currently running. Check calibrationPoint payload for point data and status of it. Stream is open and active. |
| FAILED | 1 | Calibration failed, will keep current calibration. Stream will close. |
| SUCCEEDED | 2 | Calibration was successfull. Check calibrationResult payload for result. Stream stays open for future features (improve points). Client should close it when done! |



<a name="GazeFirst-DeviceSettings-Framerate"></a>

### DeviceSettings.Framerate


| Name | Number | Description |
| ---- | ------ | ----------- |
| FPS30 | 0 | 30 Hz |
| FPS60 | 1 | 60 Hz |



<a name="GazeFirst-UserProfileRequest-OperationType"></a>

### UserProfileRequest.OperationType


| Name | Number | Description |
| ---- | ------ | ----------- |
| CREATE | 0 | Create a new user - pass username |
| UPDATE | 1 | Update (rename) an user - pass userID and username |
| DELETE | 2 | Delete an user - pass userID |
| SELECT | 3 | Select (activate) an user and its settings / calibration - pass userID |



<a name="GazeFirst-UserProfileResponse-Status"></a>

### UserProfileResponse.Status


| Name | Number | Description |
| ---- | ------ | ----------- |
| SUCCESS | 0 | Operation was successfull (CREATE, UPDATE, DELETE, SELECT) |
| NOT_FOUND | 1 | User was not found (UPDATE, DELETE, SELECT) |
| FAILED | 2 | Operation failed (CREATE) |


 

 


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
| SubscribeRawVideo | [.google.protobuf.Empty](#google-protobuf-Empty) | [RawFrame](#GazeFirst-RawFrame) stream | Subscribe to raw video frames. Client should close stream when done. |
| ManageUserProfile | [UserProfileRequest](#GazeFirst-UserProfileRequest) | [UserProfileResponse](#GazeFirst-UserProfileResponse) | Manage user profiles. |
| StreamUsers | [StreamUsersRequest](#GazeFirst-StreamUsersRequest) | [UserStreamResponse](#GazeFirst-UserStreamResponse) stream | Stream all user profiles and optionally keep the stream open for updates. |
| GetLastCalibrationResult | [.google.protobuf.Empty](#google-protobuf-Empty) | [CalibrationResult](#GazeFirst-CalibrationResult) | Get the last calibration result |

 



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

