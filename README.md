# Easy Folder Picker

Easy directory picker for Flutter  

[![pub](https://img.shields.io/pub/v/easy_folder_picker.svg)](https://pub.dev/packages/easy_folder_picker)

A flutter package to pick directories and handles requesting required permissions as well. This package only supports android.

![Picker Screenshot](screenshots/root.png)
![Picker Screenshot](screenshots/inner.png)


## Installation

Add below line to your `pubspec.yaml` and run `flutter packages get`
```
  easy_folder_picker: ^0.0.3
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

## Usage
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
