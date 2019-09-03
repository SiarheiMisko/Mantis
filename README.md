<p align="center">
    <img src="logo.png" height="80" max-width="90%" alt="Mantis" />
</p>

<p align="center">
    <img src="https://img.shields.io/badge/swift-5.0-orange.svg" alt="swift 5.0 badge" />
    <img src="https://img.shields.io/badge/platform-iOS-lightgrey.svg" alt="platform iOS badge" />
    <img src="https://img.shields.io/badge/license-MIT-black.svg" alt="license MIT badge" />   
</p>

# Mantis

   Mantis is a swift 5.0 library that mimics most interactions in the Photos.app on an iOS device. You can use the  CropViewController of Mantis with default buttons, or you can add your own buttons under the "customized" mode. 
   
<p align="center">
    <img src="Images/p1.png" height="200" alt="Mantis" />
    <img src="Images/p2.png" height="200" alt="Mantis" />
    <img src="Images/p3.png" height="200" alt="Mantis" />
    <img src="Images/p4.png" height="200" alt="Mantis" />
    <img src="Images/p5.png" height="200" alt="Mantis" />
    <img src="Images/p6.png" height="200" alt="Mantis" />
</p>

## Credits
The crop and rotation feature are strongly inspired by [TOCropViewController](https://github.com/TimOliver/TOCropViewController) and [IGRPhotoTweaks](https://github.com/IGRSoft/IGRPhotoTweaks).

The rotation dial is inspired by [10clock](https://github.com/joedaniels29/10Clock)

## Requirements
* iOS 11.0+
* Xcode 10.0+

## Install

### CocoaPods

```ruby
pod 'Mantis', '~> 0.28'
```
## Usage

* Create a cropViewController in Mantis with default config and default mode

```swift
let cropViewController = Mantis.cropViewController(image: <Your Image>)
```

* The caller needs to conform CropViewControllerProtocol
```swift
public protocol CropViewControllerProtocol: class {
    func cropViewController(_ vc: CropViewController, didGetCroppedImage image: UIImage)
    func cropViewControllerDidCanceledCroping(_ vc: CropViewController) //optional
}
```

* The caller needs to control presenting and dismissing of CropViewController. Dismissing can be controlled inside CropViewControllerProtocol methods by using 'vc'. If you didn't define method cropViewControllerDidCanceledCroping it will automatically dismiss.

* CropViewController has two modes:

  * normal mode

  In normal mode, you can use a set of standard CropViewController photo editing features.
<p align="center">
    <img src="Images/Screen Shot.png" height="300" alt="Mantis" />
</p>

```swift
let cropViewController = Mantis.cropViewController(image: <Your Image>, mode = .normal)
```

  * customizable mode
  
  This mode includes the standard cropping feature, while enabling users to customize other edit features.

<p align="center">
    <img src="Images/customizable.jpg" height="300" alt="Mantis" />
</p>

```swift
let cropViewController = Mantis.cropViewController(image: <Your Image>, mode = .customizable)
```

* Add your own ratio
```swift
            // Add a custom ratio 1:2 for portrait orientation
            let config = MantisConfig()
            config.addCustomRatio(byVerticalWidth: 1, andVerticalHeight: 2)            
            <Your ViewController> = Mantis.cropViewController(image: <Your Image>, config: config)
            
            // Set the ratioOptions of the config if you don't want to keep all default ratios
            let config = MantisConfig() 
            //config.ratioOptions = [.original, .square, .custom]
            config.ratioOptions = [.custom]
            config.addCustomRatio(byVerticalWidth: 1, andVerticalHeight: 2)            
            <Your ViewController> = Mantis.cropViewController(image: <Your Image>, config: config)
```

### Demo code

```swift
        let cropViewController = Mantis.cropViewController(image: <Your Image>, mode: .normal)
        cropViewController.delegate = self
        <Your ViewController>.present(cropViewController, animated: true)
```

<div>Icons made by <a href="https://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>


