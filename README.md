# icongen

A simple iOS icon generator that updates SVG icons within an existing project structure.

## Usage

1. Export all SVG icons from Figma into a folder (e.g. `~/Desktop/icons`).

   ```sh
   ~/Desktop/icon
     └── arrow-up.svg # 16px
     └── moon-01.svg # 24px
   ```

2. Run the script, specifying the source and destination folders:

   ```bash
   ruby ~/Projects/icongen/icongen.rb --source ~/Desktop/icons --destination ~/Projects/peaks-ios/PeaksCoreUI
   ```

3. The script creates folders grouped by icon size:

   ```
   ~/Projects/peaks-ios/PeaksCoreUI/Sources/Resources/Images.xcassets/ic/16px/
     └── ic16ArrowUp.imageset/
        └── Contents.json
        └── ic16ArrowUp.svg
     └── Contents.json

   ~/Projects/peaks-ios/PeaksCoreUI/Sources/Resources/Images.xcassets/ic/24px/
     └── ic24Moon01.imageset/
        └── Contents.json
        └── ic24Moon01.svg
     └── Contents.json
   ```

4. It also generates a `UIImage+IconGen.swift` file:

   ```swift
   extension UIImage {
       public enum ic16: String, CaseIterable {
           case arrowUp

           public func callAsFunction() -> UIImage {
               .iconInPackage(name: rawValue, size: 16, bundle: .module)
           }
       }

       public enum ic24: String, CaseIterable {
           case moon01

           public func callAsFunction() -> UIImage {
               .iconInPackage(name: rawValue, size: 24, bundle: .module)
           }
       }
   }
   ```

5. Use icons like this in your app:

   ```swift
   button.setImage(.ic16.arrowUp())
   button.setImage(.ic24.moon01())
   ```

6. Add script as alias

   ```sh
   alias icongen="ruby /Users/peaks/Projects/icongen/icongen.rb --source ~/Desktop/icons --destination ~/Projects/peaks-ios/PeaksCoreUI"
   ```
