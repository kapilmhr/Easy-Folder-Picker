# Easy Folder Picker

Easy directory picker for Flutter

[![pub](https://img.shields.io/pub/v/easy_folder_picker.svg)](https://pub.dev/packages/easy_folder_picker)

A flutter package to pick directories and handles requesting required permissions as well.
This package only supports **ANDROID**.

![Picker Screenshot1](https://github.com/kapilmhr/Easy-Folder-Picker/blob/main/screenshots/root.png)
![Picker Screenshot2](https://github.com/kapilmhr/Easy-Folder-Picker/blob/main/screenshots/inner.png)


## Installation

Add below line to your `pubspec.yaml` and run `flutter packages get`
```
  easy_folder_picker: ^latest version
```

## Permissions
Add below line to your `android/app/src/main/AndroidManifest.xml`
```
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```
If you want to allow creating new folders directly from picker then add the below permission also
```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```
#### Android 10 (Q)
In Android 10, you need to add the Following Lines in AndroidManifest file:
```
<application
      android:requestLegacyExternalStorage="true"
```
#### Android 11
From Android 11, you need to manage permission within your app, if you want to write in different folders of **external storage**.
- Add the following Lines in AndroidManifest file
```
  <uses-permission android:name="android.permission.MANAGE_EXTERNAL_STORAGE"/>
```
- Add [device_info](https://pub.dev/packages/device_info) package to check android version
- Check permission if app can **manage external storage** if its android 11 or greater
```
  var status = await Permission.storage.status;
      if (status!.isRestricted) {
        status = await Permission.storage.request();
      }

      if (status!.isDenied) {
        status = await Permission.storage.request();
      }
      if (status!.isPermanentlyDenied) {
        ScaffoldMessenger.of(context).showSnackBar(SnackBar(
          backgroundColor: Colors.green,
          content: Text('Please add permission for app to manage external storage'),
        ));
      }
```
# Flutter Usage
```
import 'package:easy_folder_picker/FolderPicker.dart';

// In any callback call the below method
  Future<void> _pickDirectory(BuildContext context) async {
    Directory directory = selectedDirectory;
    if (directory == null) {
      directory = Directory(FolderPicker.ROOTPATH);
    }

    Directory newDirectory = await FolderPicker.pick(
        allowFolderCreation: true,
        context: context,
        rootDirectory: directory,
        shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.all(Radius.circular(10))));
    setState(() {
      selectedDirectory = newDirectory;
      print(selectedDirectory);
    });
  }
```
