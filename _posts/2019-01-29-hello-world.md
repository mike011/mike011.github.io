---
title: "Welcome to Jekyll!"
published: true
---

**Hello world**, this is my first Jekyll blog post.

I hope you like it!

I’m Michael. I’ve been working with computers for most of my life. Starting with Commodore-64 and doing LOAD "*",8,1 up until now working on fancy iPhones and MacBooks. These new machine are hundreds of thousands of time more powerful that what I used before.

Most of my younger years were playing games and just having fun. I didn’t seriously think about a future in computers until my high school days where I started digging into more how computers work by building them at school and at home. I was set and went to University for Computer Science. It was a great four years. I definitely found that I wanted to do software and not hardware. Hardware was way too much physics for me.

After school I started in QA and moved to automated testing, then to development, then back to automated QA, and most recently back to development. Great times.

Below points out how highlighting look for various languages I work in.

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
