# image-processing-in-java
In the introductory set on Image Processing, BufferedImage class of Java was used for processing images the applications of BufferedImage class is limited to some operations only, i.e, we can modify the R, G, B values of given input image and produce the modified image. For complex image processing such as face/object detection OpenCV library is used which we will use in this article.

At first we need to setup OpenCV for Java, we recommend to use eclipse for the same since it is easy to use and setup.

Now lets understand some of the methods required for face detection.

CascadeClassifier() : This class is used to load the trained cascaded set of faces which we will be using to detect face for any input image.
Imcodecs.imread()/Imcodecs.imwrite() : These methods are used to read and write images as Mat objects which are rendered by OpenCV.
Imgproc.rectangle() : Used to generate rectangle box outlining faces detected, it takes four arguments – input_image, top_left_point, bottom_right_point, color_of_border.
// Java program to demonstrate face detection 
package ocv; 
  
import org.opencv.core.Core; 
import org.opencv.core.Mat; 
import org.opencv.core.MatOfRect; 
import org.opencv.core.Point; 
// Java program to demonstrate face detection 
package ocv; 
  
import org.opencv.core.Core; 
import org.opencv.core.Mat; 
import org.opencv.core.MatOfRect; 
import org.opencv.core.Point; 
import org.opencv.core.Rect; 
import org.opencv.core.Scalar; 
import org.opencv.imgcodecs.Imgcodecs; 
import org.opencv.imgproc.Imgproc; 
import org.opencv.objdetect.CascadeClassifier;
public class FaceDetector 
{ 
    public static void main(String[] args) 
    { 
  // Face detector creation by loading source cascade xml file 
        // using CascadeClassifier. 
        // the file can be downloade from 
        // https://github.com/opencv/opencv/blob/master/data/haarcascades/ 
        // haarcascade_frontalface_alt.xml 
        // and must be placed in same directory of the source java file 
        CascadeClassifier faceDetector = new CascadeClassifier(); 
        faceDetector.load("haarcascade_frontalface_alt.xml"); 
        // For proper execution of native libraries 
        // Core.NATIVE_LIBRARY_NAME must be loaded before 
        // calling any of the opencv methods 
        System.loadLibrary(Core.NATIVE_LIBRARY_NAME); 
  
 // Input image 
        Mat image = Imgcodecs.imread("E:\\input.jpg"); 
   // Detecting faces 
        MatOfRect faceDetections = new MatOfRect(); 
        faceDetector.detectMultiScale(image, faceDetections); 
  
// Creating a rectangular box showing faces detected 
        for (Rect rect : faceDetections.toArray()) 
        { 
            Imgproc.rectangle(image, new Point(rect.x, rect.y), 
             new Point(rect.x + rect.width, rect.y + rect.height), 
                                           new Scalar(0, 255, 0)); 
        } 
 // Saving the output image 
        String filename = "Ouput.jpg"; 
        Imgcodecs.imwrite("E:\\"+filename, image); 
    } 
} 
