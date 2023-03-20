## Github SSH key
* [Generating a new SSH key.](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agen)
* [Adding your SSH key to the ssh-agent.](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agen)
* [Adding a new SSH key to your account.](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?tool=webui#adding-a-new-ssh-key-to-your-account)

## [Homebrew](https://brew.sh/)
* Install Homebrew
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
## [Fastlane](https://docs.fastlane.tools/getting-started/ios/setup/#)
* Install fastlane
```
brew install fastlane
```
* Navigate your terminal to your project's directory
```
cd ./PATH/cicd-example
```
* Setting up fastlane
```
fastlane init
```
* Choose setup
```
[22:43:37]: -----------------------------
[22:43:37]: --- Welcome to fastlane 🚀 ---
[22:43:37]: -----------------------------
[22:43:37]: fastlane can help you with all kinds of automation for your mobile app
[22:43:37]: We recommend automating one task first, and then gradually automating more over time
[22:43:37]: What would you like to use fastlane for?
1. 📸  Automate screenshots
2. 👩‍✈️  Automate beta distribution to TestFlight
3. 🚀  Automate App Store distribution
4. 🛠  Manual setup - manually setup your project to automate your tasks
?  4
```
* Config Fastfile
```
platform :ios do
  desc "Build Test Flight"
  # Deletes files archives as result
  before_all do
      sh(command: "rm -vfr ~/Library/Developer/Xcode/Archives/*")
      clear_derived_data()
      xcode_select("/Applications/Xcode.app")
  end

  # release build
  lane :release do
    match(type: "appstore", 
          app_identifier: "mobile.duc.***",
          readonly: is_ci)
    increment_build_number(xcodeproj: "cicd-example.xcodeproj")
    build_app(
      scheme: "MobileCiCd",
      export_method: "app-store"
    )
    upload_to_testflight
  end

  # Deletes files created as result of running gym, cert, sigh or download_dsyms
  after_all do |lane|
      clean_build_artifacts
  end
end
```
## [Matchfile](https://docs.fastlane.tools/actions/match/)
* Install matchfile
```
fastlane match init
```
* Choose setup
```
[✔] 🚀 
[14:03:49]: fastlane match supports multiple storage modes, please select the one you want to use:
1. git
2. google_cloud
3. s3
4. gitlab_secure_files
?  1
[14:03:55]: Please create a new, private git repository to store the certificates and profiles there
[14:03:55]: URL of the Git Repo: git@github.com:nmduc2511/cert-provision-cicd.git
[14:08:38]: Successfully created './fastlane/Matchfile'. You can open the file using a code editor.
[14:08:38]: You can now run `fastlane match development`, `fastlane match adhoc`, `fastlane match enterprise` and `fastlane match appstore`
```
* Config match file
```
git_url("git@github.com:nmduc2511/cert-provision-cicd.git")

storage_mode("git")

type("appstore") # The default type, can be: appstore, adhoc, enterprise or development

app_identifier("mobile.duc..cicd-example") # bundle id app
username("n*****@gmail.com") # Your Apple Developer Portal username
```
* To set up the certificates and provisioning profiles on a new machine
```
fastlane match appstore
```
* You can also run match in a readonly mode to be sure it won't create any new certificates or profiles.
```
fastlane match appstore --readonly
```
* Or setup in ./fastlane/Fastfile (**Recommend**)
```
lane :appstore do
  match(type: "appstore", readonly: is_ci)
end
```
###### ... result
```
[14:19:40]: ▸ -----END CERTIFICATE-----
[14:19:41]: Downloading provisioning profile...
[14:19:41]: Successfully downloaded provisioning profile...
[14:19:41]: Installing provisioning profile...
/var/folders/2h/7rqr0mfn7kd735ws6yl9plb00000gq/T/d20230316-26095-3eh5kt/profiles/appstore/AppStore_mobile.duc..cicd-example.mobileprovision
[14:19:42]: Installing provisioning profile...
[14:19:45]: 🔒  Successfully encrypted certificates repo
[14:19:45]: Pushing changes to remote git repo...
[14:19:50]: Finished uploading files to Git Repo [git@github.com:nmduc2511/cert-provision-cicd.git]
+---------------------+-----------------------------------------+-----------------------------------------+
|                                     Installed Provisioning Profile                                      |
+---------------------+-----------------------------------------+-----------------------------------------+
[14:19:50]: All required keys, certificates and provisioning profiles are installed 🙌
```
* Repos Git
![github_repo](https://user-images.githubusercontent.com/114910830/225548884-2a8576da-5c57-410d-9d12-cc9df95b5f26.png)

## [Authenticating with Apple services](https://docs.fastlane.tools/getting-started/ios/authentication/)
* Visit [appleid.apple.com/account/manage](https://appleid.apple.com/account/manage)
* Generate a new application specific password
* Provide the application specific password using the environment variable FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD
* Generate .env(**environment**)
```
touch .env
```
* Config .env file
```
FASTLANE_USER= // apple userid
FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD=***-***-***-***
```
## Config Runner To Run self-hosted
* [Adding self-hosted runners](https://docs.github.com/en/actions/hosting-your-own-runners/adding-self-hosted-runners)
