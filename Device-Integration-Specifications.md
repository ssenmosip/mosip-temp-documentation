# Device Integration approach:

This document detailed out the design approach to integrate with the list of devices used in the MOSIP platform.

Interface approach has been taken to implement the integration with external devices. The interface should have the required method to communicate with the external devices. The respective device vendor's specific implementation class should implement the methods using vendor provided libraries. An Abstract class also been defined to provide the common utility feature required at device level irrespective of vendor based implementation.

## Devices:
1. Scanner
2. Printer
3. Web Camera
4. GPS

### Scanner: 
**Interface Class: IMosipDocumentScannerService**  
   1. public Boolean isConnected()  -Method declaration which has to be implemented based on  Device/Platform to check the scanner connection availability.
   
   2. public BufferedImage scan() -  Method declaration which has to be implemented based on  Device/Platform to scan the document from the scanner device.  

**Abstract Class: DocumentScannerService**  
1. public byte[] asPDF(List<BufferedImage> bufferedImages) –  Method Implementation to convert the captured scanned document files into pdf format.  

2. public byte[] asImage(List<BufferedImage> bufferedImages) - Method Implementation to convert the captured scanned document files into image format.  

3. public byte[] getImageBytesFromBufferedImage(BufferedImage bufferedImage) – Method Implementation to get the byte[] from BuffredImage object.  

4. public List<BufferedImage>  pdfToImages(byte[] pdfBytes) – Method Implementation to convert the pdf document to image format in order to show in the document preview.  

 
### Web Camera:  
**Interface Class:IMosipWebcamService**   
1. public boolean connect(int width, int height)  
   This method is used to open the web camera (there is device specific implementation for this interface) from the list of webcams with specified device name and specified resolution.  
**_Parameters:_**  
width - required width for the camera to be set-up  
height - required height for the camera to be set-up  

2. public BufferedImage captureImage()  
   This method captures the image from webcam and returns it. If the webcam is closed or has been already disposed by JVM, it returns null.  

3. public void close()
   This method is to close the webcam which is opened.

**Abstract Class:**  MosipWebcamServiceImpl

### GPS:  
**Interface Class:MosipWebcamProvider**   
**Abstract Class:**  

