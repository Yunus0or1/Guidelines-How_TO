# Windows Installation

 - First download flutter by searching from Google.
 - Install the zip file or whatever they provide you.
 - Now to add flutter in cmd, open up Environment Variables by searching 'Environment' in windows search bar.
 - Double click on PATH in System variables and add your path. It must include bin folder. For example it can be 'C:\Flutter\bin'
 - Restart your cmd.
 - Install Android Studio. It will prompt for some packages to install for Flutter. Install these.
 - Open up cmd and write this command.
   ```
   flutter doctor
   ```
  If everything shows correctly with no error than flatter is installed properly.
 - To start a new project in Flutter, open up cmd, browse to a directory and write this command 
   ```
   flutter create project_name
   ```   
 - To run a project from cmd first of all plug your real android device or open up emulator device. Browse to the project directory.for example : ***cd /d D:/folder/firstapp*** and write this command 
   ```
   flutter run
   ```
   To Hot Reload in CMD , press 'r'
   To restart the app again press 'R'
   
# Get SHA-1, MD5 fingerprints

 - Open your project in Android Studio.
 - Unfold it.
 - Right click on Android folder and press 'Open in Terminal'
 - Press Enter in Terminal once and paste this command.
   ```
   gradlew signingReport
   ```
   It will show you all the fingerprints and verifications.

# Clean cache in flutter.
  ```
  flutter packages pub cache clean
  pub cache repair
  ```

# Install the Flutter and Dart plugins
  ```
  Start Android Studio.
  Open plugin preferences (File > Settings > Plugins on Windows & Linux).
  Select Browse repositories, select the Flutter plugin and click Install.
  Click Yes when prompted to install the Dart plugin.
  Click Restart when prompted.
  ```
  


   
