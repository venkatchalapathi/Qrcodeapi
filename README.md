# Qrcodeapi


# Dependency section


        implementation 'com.google.android.gms:play-services:9.8.0'
   
   
   
# Add xml code 

   
       
 To display the output here i have taken a TextView
 
     <SurfaceView
       android:layout_width="match_parent"
       android:layout_height="400dp"
       android:id="@+id/surface"
       android:layout_centerInParent="true"/>
       
      <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/result_text"
        android:gravity="center"
        android:id="@+id/textview"
        android:layout_below="@+id/surface"/>
        
        
  Define Globally 
  
      SurfaceView surfaceView;
      TextView textView;
      BarcodeDetector barcodeDetector;
      CameraSource cameraSource;
      final int requestid = 100;
      
      
 Overrride onRequestPermissionsResult() Method
 
      @Override
      public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        switch (requestCode) {
            case requestid:
                if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                    if (ActivityCompat.checkSelfPermission(this, Manifest.permission.CAMERA) != PackageManager.PERMISSION_GRANTED) {

                        return;
                    }
                    try {
                        cameraSource.start(surfaceView.getHolder());
                    } catch (IOException e) {

                    }
                }
        }
    }
    
    # Instanciate and find the views global references in onCreate method
    
       surfaceView = (SurfaceView) findViewById(R.id.surface);
        textView = (TextView) findViewById(R.id.textview);
        barcodeDetector = new BarcodeDetector.Builder(this)
                .setBarcodeFormats(Barcode.QR_CODE)
                .build();
        cameraSource = new CameraSource.Builder(this, barcodeDetector)
                .setRequestedPreviewSize(640, 480).build();
