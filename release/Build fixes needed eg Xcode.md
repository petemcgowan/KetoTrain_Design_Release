I'm following these instructions on the Firebase side to setup Firebase, because just the plist being added to the root doesn't do it, so it may well need this?  That's the current theory...
https://rnfirebase.io/#3-ios-setup


---------------------------------------------------

THE ERROR: 
'value' is unavailable: introduced in iOS 12.0.

The SOLUTION:
post_install do |installer|
   installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|
               config.build_settings['SWIFT_VERSION'] = '5.0'
               config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '12.4'
       end
   end
end

This is what I ended up merging into my Podfile:

  post_install do |installer|
    react_native_post_install(installer)
    __apply_Xcode_12_5_M1_post_install_workaround(installer)
    installer.pods_project.targets.each do |target|
         target.build_configurations.each do |config|
                config.build_settings['SWIFT_VERSION'] = '5.0'
                config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '12.4'
        end
    end
  end
  

  
---------------------------------------------------
THE ERROR: unary_function and binary_function are no longer provided in C++17 and newer Standard modes. 


The SOLUTION":
Open your project in Xcode.
Navigate to the Pods project in the Project Navigator.
Select the appropriate target that's failing (probably the library that includes boost).
Go to the Build Settings tab.
Search for Preprocessor Macros or GCC_PREPROCESSOR_DEFINITIONS.
Add _LIBCPP_ENABLE_CXX17_REMOVED_UNARY_BINARY_FUNCTION to both Debug and Release (or any other configurations you have).


This will be removed **every time** you do a pod install or touch the podfile, so it will need to be re-added

---------------------------------------------------
The Firebase ad tracking thing:

$RNFirebaseAnalyticsWithoutAdIdSupport=true

Should be added like this to the podfile:


...production = ENV["PRODUCTION"] == "1"

$RNFirebaseAnalyticsWithoutAdIdSupport = true

pre_install do |installer|....