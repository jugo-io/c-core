# Unreal Engine integration

Our C-core SDK can be used together with [Unreal Engine](https://www.unrealengine.com/en-US). It's **not** a fully functional plugin yet, but can easily be integrated into your project as a [Unreal Engine Module](https://docs.unrealengine.com/5.3/en-US/unreal-engine-modules/).

## How to setup PubNub C-Core SDK as a Unreal Engine Module

1. Clone this repository to the `<UnrealProject>/Source/` directory. We recommend that you place it inside the `ThirdParty` folder (create it, if necessary). 

2. Compile the [desired option](https://www.pubnub.com/docs/sdks/c-core#hello-world) of the SDK. You can do it in the SDK directory like so:
  
  - POSIX:

    ```sh
    make -C <option> -f <architecture>.mk pubnub_<implementation>.a 
    ```
    
  - Windows:

    ```sh
    nmake -f windows.mk
    ```

  - Windows Universal Platform:

    ```sh
    nmake -f windows/uwp.mk
    ```

    Windows builds everything at once. We are aware that our build system needs some love.

    For example, to build the OpenSSL option, run the following script:
  
    ```sh
    make -C openssl -f posix.mk pubnub_sync.a
    ```
    
    :warning: If you choose `openssl`, ensure that your OpenSSL library headers match the Unreal ones!
  
3. Adjust `PubNubModule/PubNubModule.Build.cs` with selected options by changing `option`, `architecture` and `implementation` with the same values you used for compilation. 

  > This is a temporary solution. We are aware that our build system needs some love.

  For example:
  
  ```csharp 
  private readonly string Option = "openssl"; // posix, windows, openssl
  private readonly string Architecture = "posix"; // posix, windows
  private readonly string string Implementation = "sync"; // sync, callback
  ```

4. Finally, import the module into your project as follows:

  - `<UnrealProject>.Target.cs` and `<UnrealProject>Editor.Target.cs`
  
    ```csharp
    public class <UnrealProject>[Editor]Target : TargetRules
    {
      public <UnrealProject>[Editor]Target (TargetInfo Target) : base(Target)
      {
        //...
        ExtraModuleNames.Add("PubNubModule");
      }
    }
    ```
  
  - `<UnrealProject>.uproject`
  
    ```json
    {
      //...
      "Modules": [
        //...
        {
          "Name": "PubNubModule",
          "Type": "Runtime",
          "LoadingPhase": "Default"
        }
      ],
      //...
    }
    ```

Generate the project files using your IDE of choice and you are ready to go!

## Usage 

1. Make PubNub discoverable in the module you want to use PubNub in by modifying the `<Module>.Build.cs` file:

  ```csharp
  public class <Module> : ModuleRules
  {
    public <Module>(ReadOnlyTargetRules Target) : base(Target)
    {
      //...
      PrivateDependencyModuleNames.Add("PubNubModule");
    }
  }
  ```

2. Import the `PubNub.h` header into your files as follows:
  
  ```cpp
  #include "PubNub.h" 
  ```

  > Note that you don't have to wrap it with `THIRD_PARTY_INCLUDES_START` and `THIRD_PARTY_INCLUDES_END` because we've done that for you.

Good luck with your project!

