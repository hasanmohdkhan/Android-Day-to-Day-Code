```

       //checking for permission if not granted then show a toast
        permissionCheck();
        
        //if permission is granted then add music to list
        if (isPermissionGranted()) {
            addMusic();
        }
        
        
private void permissionCheck() 
      {
        if (ActivityCompat.checkSelfPermission(this, Manifest.permission.READ_EXTERNAL_STORAGE)
                != PackageManager.PERMISSION_GRANTED) {
            Toast.makeText(getApplicationContext(), R.string.permission_required_str, Toast.LENGTH_SHORT).show();
            return;
        }
       }
    
 @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String permissions[], @NonNull int[] grantResults) {
        switch (requestCode) {
            case 1: {
                if (grantResults.length > 0
                        && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                    Toast.makeText(getApplicationContext(), R.string.permission_granted_str, Toast.LENGTH_SHORT).show();
                    addMusic();
                } else {
                    Toast.makeText(getApplicationContext(), R.string.permission_deny_str, Toast.LENGTH_SHORT).show();
                    finish();
                }
            }
        }
    }  
    
    public boolean isPermissionGranted() {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            if (checkSelfPermission(Manifest.permission.READ_EXTERNAL_STORAGE)
                    == PackageManager.PERMISSION_GRANTED) {
                return true;
            } else {
                ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.READ_EXTERNAL_STORAGE}, 1);
                return false;
            }
        } else { //permission is automatically granted on sdk<23 upon installation
            return true;
        }
    }
	
	```
	