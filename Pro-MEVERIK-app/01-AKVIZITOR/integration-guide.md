# Integration Guide for RoomPlan API in AKVIZITOR App

## Table of Contents
1. [Introduction](#introduction)
2. [Virtual Tour Creation](#virtual-tour-creation)
3. [3D Property Scanning Setup](#3d-property-scanning-setup)
4. [Real Estate Portal Export](#real-estate-portal-export)

## Introduction
This guide provides a comprehensive step-by-step process for integrating the RoomPlan API into the AKVIZITOR app. Follow these instructions to set up virtual tours, conduct 3D property scans, and export data for real estate portals.

## Virtual Tour Creation
1. **Access the RoomPlan API**: Start by accessing the RoomPlan API documentation to understand the available endpoints and authentication methods.
2. **Set up API Key**: Register your application with RoomPlan to obtain an API key.
3. **Initialize API Client**: Use the API key to initialize the API client in your application.
4. **Create a Virtual Tour**: 
   - Use the `POST /virtual-tours` endpoint to create a new virtual tour.
   - Provide necessary parameters such as property details, images, and floor plans.
5. **Review and Publish**: Once created, review the virtual tour details and publish it for public access.

## 3D Property Scanning Setup
1. **Download the Required SDK**: Get the RoomPlan SDK needed for property scanning setup.
2. **Configure Your Device**: Ensure that your device is compatible and configured for 3D scanning.
3. **Start Scanning**: Activate the scanning feature within the AKVIZITOR app and follow on-screen instructions to scan the property.
4. **Save and Process Data**: Once the scan is complete, save the data and process it for integration.

## Real Estate Portal Export
1. **Select Export Options**: From the AKVIZITOR app, select the properties you want to export.
2. **Choose Format**: Decide the format for the export (e.g., JSON, XML).
3. **Initiate Export**: Use the `GET /export` endpoint to initiate the export of selected properties to the specified format.
4. **Download Exported Data**: Once the process is complete, download the exported files for upload to the real estate portal.

## Conclusion
Follow these steps to successfully integrate the RoomPlan API into your AKVIZITOR app, enabling functionalities like virtual tours, property scanning, and data exports for real estate purposes.