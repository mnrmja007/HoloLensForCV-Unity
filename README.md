# HoloLensForCV-Unity
HoloLens research mode streams made available for use in Unity through [IL2CPP Windows Runtime support](https://docs.unity3d.com/2018.4/Documentation/Manual/IL2CPP-WindowsRuntimeSupport.html). See my [blog post](https://doughtmw.github.io/posts/HoloLensForCV-Unity-1) for more information on the sample.

Incorporates:
- [HoloLensForCV](https://github.com/microsoft/HoloLensForCV) sample from Microsoft 
- [depthPvMapper](https://github.com/cyberj0g/HoloLensForCV/blob/master/Samples/ComputeOnDevice/DepthPvMapper.cpp) from cyberj0g

![Pv depth camera sample](https://github.com/doughtmw/HoloLensForCV-Unity/blob/master/HoloLens-PvDepth-Example.jpg)

## Requirements
- Tested with [Unity 2018.4 LTS](https://unity3d.com/unity/qa/lts-releases
)
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
- Minimum [RS4](https://docs.microsoft.com/en-us/windows/mixed-reality/release-notes-april-2018), tested with [OS Build 17763.678](https://support.microsoft.com/en-ca/help/4511553/windows-10-update-kb4511553)
- HoloLens with **research mode enabled**

## Sensor Stream Sample
1. Open HoloLensForCV sample in VS2017 and install included OpenCV nuget package to HoloLensForCV project
2. Build the HoloLensForCV project (x86, Debug or Release) 
3. Copy all output files from HoloLensForCV output path (dlls and HoloLensForCV.winmd) to the Assets->Plugins->x86 folder of the HoloLensForCVUnity project
4. Open HoloLensForCVUnity Unity project and build using IL2CPP, allow unsafe code under Unity Player Settings->Other Settings
5. Navigate to Unity project build folder and modify the Package.appxmanifest file to include: 
- Restricted capabilities package:
```xml 
<Package 
  xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
  xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2" 
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3" 
  xmlns:uap4="http://schemas.microsoft.com/appx/manifest/uap/windows10/4" 
  xmlns:iot="http://schemas.microsoft.com/appx/manifest/iot/windows10" 
  xmlns:mobile="http://schemas.microsoft.com/appx/manifest/mobile/windows10" 
  xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities" 
  IgnorableNamespaces="uap uap2 uap3 uap4 mp mobile iot rescap" 
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"> 
```
- Modified capabilities with with new package:
```xml
  <Capabilities>
    <rescap:Capability Name="perceptionSensorsExperimental" />
    <Capability Name="internetClient" />
    <Capability Name="internetClientServer" />
    <Capability Name="privateNetworkClientServer" />
    <uap2:Capability Name="spatialPerception" />
    <DeviceCapability Name="webcam" />
  </Capabilities>
```
6. Open VS solution, build then deploy to device
