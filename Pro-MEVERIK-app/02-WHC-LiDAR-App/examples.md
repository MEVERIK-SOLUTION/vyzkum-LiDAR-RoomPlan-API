# RoomPlan API Integration into WHC-LiDAR-App

This document provides practical code examples for integrating the RoomPlan API into the WHC-LiDAR-App, including Swift implementations for scanning, processing 3D data, and exporting to DWG/IFC formats.

## 1. Scanning with RoomPlan API

```swift
import RoomPlan

let scanSession = RoomPlan.ScanSession()
scanSession.start() 
// Use appropriate delegate methods to handle results and errors.
```

## 2. Processing 3D Data

After scanning, you can process the captured 3D data:

```swift
let roomData = scanSession.roomData
// Process roomData to extract information, e.g., dimensions, surface types.
```

## 3. Exporting to DWG/IFC Formats

To export processed data to DWG/IFC formats:

```swift
let exporter = RoomPlan.Exporter()
exporter.exportToDWG(roomData)
exporter.exportToIFC(roomData)
```

## Conclusion

Integrating the RoomPlan API allows for seamless scanning, processing, and exporting of 3D data into various formats, making it essential for applications like WHC-LiDAR-App.