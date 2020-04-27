---
title: "Welcome to Jekyll!"
published: true
---

**Hello world**, this is my first Jekyll blog post.

I hope you like it! It's pointing out how highlighting look for various languages I work in.

# Highlighter

## Swift
```swift
print("Hello World")
```

## Objective-C
```swift
NSLog(@"Hello World")
```

## Fastlane
```ruby
lane :ci_build do
  sh "rm -rf build"

  xcodebuild(
    clean: true,
    archive: true,
    archive_path: './build/BanditTheCat.xcarchive',
    workspace: ENV['WORKSPACE'],
    scheme: ENV['SCHEME'],
    configuration: 'Release',
    sdk: 'iphoneos',
    )
end
```

## Console

```
# "Get the directory that this script file exists in."
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"

print_section_title "Changing to project directory ${WORKSPACE}/BuildDir/"
cd ${WORKSPACE}/BuildDir/

# Download tools to be used while building
download_tools

# Build the project
bundle exec fastlane build
```


## Circle CI
```yaml
  version: 2
  jobs:
    build:
      docker:
        - image: circleci/<language>:<version TAG>
      steps:
        - checkout
        - run: <command>
...
```
