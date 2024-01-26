* Bookmarks
** Asset Naming Conventions
https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/AssetNaming/

** Download UE4 assets from the Epic Games Marketplace using Linux
https://alexandra-zaharia.github.io/posts/download-from-unreal-engine-4-marketplace-in-linux/
https://www.reddit.com/r/linux_gamedev/comments/ms1vai/unreal_engine_4_marketplace_on_linux/
https://blog.gamedev.tv/ue4-marketplace-linux/

** Linux Quick Start, Learn how to download, build, and run UE4 on Linux.
https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Linux/BeginnerLinuxDeveloper/SettingUpAnUnrealWorkflow/

* Install on PopOS
** Install libssl1.1
*** echo "deb http://security.ubuntu.com/ubuntu impish-security main" | sudo tee /etc/apt/sources.list.d/impish-security.list
*** sudo apt update
*** sudo apt install libssl1.1
** Install Android SDK
*** sudo apt update android-sdk
** Edit Bashrc
*** export ANDROID_HOME=$HOME/Android/Sdk
*** export PATH=$PATH:$ANDROID_HOME/tools
*** export PATH=$PATH:$ANDROID_HOME/platform-tools
** ./Setup.sh
** ./GenerateProjectFiles.sh
** make