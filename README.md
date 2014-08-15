# ISLocation.framework

`ISLocation.framework` is an iOS framework providing interfaces for determining a user’s location based on ISP's proprietary BLE beacon platform.

## Downloading the Framework

`ISLocation.framework` can be downloaded in a ZIP file from [here](https://github.com/IntelligentSpatialPositioning/ISLocation/releases/download/intial/ISLocation.framework.zip). 

The framework needs to then be placed in a subdirectory beneath your app.

## Embedding in an iOS Application

Once `ISLocation.framework` has been placed in a subdirectory beneath your app, drag it into your Xcode project; it will show up as a linked framework.

Add the following additional frameworks to your project by clicking on your Target, choosing the "Build Phases" tab, and using the `+` button at the bottom of the "Linked Libraries" section:

* CoreMotion
* CoreLocation
* ISLocation

[ISLocationDemoApp](https://github.com/IntelligentSpatialPositioning/ISLocationDemoApp) is an example of an iOS application built using `ISLocation.framework`.

### External Dependencies

[JSONKit](https://github.com/johnezang/JSONKit) is required for JSON parsing within the framework.

JSONKit can be downloaded in a ZIP file from [here](https://github.com/johnezang/JSONKit/archive/master.zip). Once you have downloaded and unzipped the ZIP file, you will need to drop JSONKit.h and JSONKit.m in your Xcode project.

JSONKit needs some specific compile flags. To set these do the following;

1. Go to your Xcode project settings, under Build Phases > Compile Sources
2. Select JSONKit and add `-fno-objc-arc -Wno-deprecated-objc-isa-usage` as compiler flags. 

## Using ISLocation

Use of ISLocation requires an account for ISP's cloud-location platform, for further details on this please [contact us](mailto:support@intelligentspatialpositioning.com).

Once a space has been trained using ISP's iOS training application, the UUID for the desired training instance needs to be noted. This can be found under Space>[Name of Space]>Trainings>Info

The specified training UUID needs to be used when instantiating ISLocation within an iOS application as follows;

(Note that `a2873c78-1fa5-3ea6-61e1-92e345d305ba` should be replaced with the training UUID you want to use)

```objective-c
NSUUID *token = [[NSUUID alloc] initWithUUIDString:@"a2873c78-1fa5-3ea6-61e1-92e345d305ba"];
_location = [[ISLocation alloc] initWithToken:token delegate:self];
```

The following callback will then deliver a list of each zone that exists within your training, along with the probability of the user being in each zone.

```objective-c
- (void)location:(ISLocation *)location didChangeZoneScores:(NSArray *)zoneScores {
    NSLog(@"%@", zoneScores);
}
```

## Support

`ISLocation.framework` is fully supported by Intelligent Spatial Positoning. If you have any questions, comments, or bug reports, please contact us at [support@intelligentspatialpositioning.com](mailto:support@intelligentspatialpositioning.com).
