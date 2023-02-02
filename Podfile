use_frameworks!

def all_example_pods
  pod 'SDWebImage/MapKit', :path => './'
  pod 'SDWebImageWebPCoder', :git => 'https://github.com/SDWebImage/SDWebImageWebPCoder.git', :branch => 'master'
end

def watch_example_pods
  pod 'SDWebImage/Core', :path => './'
  pod 'SDWebImageWebPCoder', :git => 'https://github.com/SDWebImage/SDWebImageWebPCoder.git', :branch => 'master'
end

def all_test_pods
  pod 'SDWebImage/MapKit', :path => './'
  pod 'Expecta'
  pod 'KVOController'
  pod 'SDWebImageWebPCoder', :git => 'https://github.com/SDWebImage/SDWebImageWebPCoder.git', :branch => 'master'
end

example_project_path = 'Examples/SDWebImage Demo'
test_project_path = 'Tests/SDWebImage Tests'
workspace 'SDWebImage.xcworkspace'

# Example Project
target 'SDWebImage iOS Demo' do
  project example_project_path
  platform :ios, '9.0'
  all_example_pods
end

# Inject macro during SDWebImage Demo and Tests
post_install do |installer_representation|
  installer_representation.generated_pod_targets.each do |target|
    if target.pod_name == "SDWebImage"
      build_settings = target.build_settings
      build_settings.each do |configuration, build_setting|
        if configuration == :debug
          config = build_setting.xcconfig
          old_value = config.attributes['GCC_PREPROCESSOR_DEFINITIONS']
          config.attributes['GCC_PREPROCESSOR_DEFINITIONS'] = old_value + ' SD_CHECK_CGIMAGE_RETAIN_SOURCE=1'
          config.save_as(target.xcconfig_path(configuration))
        end
      end
    end
  end
end
