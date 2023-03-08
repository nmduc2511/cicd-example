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
