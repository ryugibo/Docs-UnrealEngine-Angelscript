+++
title = "Subsystems"
weight = 140
+++

# Subsystems

Subsystems are one of unreal's ways to collect common functionality into easily accessible singletons.
See the [Unreal Documentation on Programming Subsystems](https://docs.unrealengine.com/5.1/en-US/programming-subsystems-in-unreal-engine/) for more details.

## Using a Subsystem

Subsystems in script can be retrieved by using `USubsystemClass::Get()`.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">TestCreateNewLevel</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">auto</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">LevelEditorSubsystem</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">ULevelEditorSubsystem</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">Get</span><span style="color: #d4d4d4;">();</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">LevelEditorSubsystem</span><span style="color: #d4d4d4;">.</span><span style="color: #dcdcaa;">NewLevel</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"/Game/NewLevel"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

> **Note:** Many subsystems are _Editor Subsystems_ and cannot be used in packaged games.  
> Make sure you only use editor subsystems inside [Editor-Only Script](@/scripting/editor-script.md).

## Creating a Subsystem

To allow creating subsystems in script, helper base classes are available to inherit from that expose overridable functions.  
These are:

- `UScriptWorldSubsystem` for world subsystems
- `UScriptGameInstanceSubsystem` for game instance subsystems
- `UScriptLocalPlayerSubsystem` for local player subsystems
- `UScriptEditorSubsystem` for editor subsystems
- `UScriptEngineSubsystem` for engine subsystems

For example, a scripted world subsystem might look like this:

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">UMyGameWorldSubsystem</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">UScriptWorldSubsystem</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">Initialize</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">Print</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"MyGame World Subsystem Initialized!"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">Tick</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">DeltaTime</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">Print</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"Tick"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">// Create functions on the subsystem to expose functionality</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">LookAtMyActor</span><span style="color: #d4d4d4;">(</span><span style="color: #4ec9b0;">AActor</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">Actor</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><div><span style="color: #d4d4d4;">}</span></div><br><div><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">UseMyGameWorldSubsystem</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">auto</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">MySubsystem</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">UMyGameWorldSubsystem</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">Get</span><span style="color: #d4d4d4;">();</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">MySubsystem</span><span style="color: #d4d4d4;">.</span><span style="color: #dcdcaa;">LookAtMyActor</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">nullptr</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

Any `UFUNCTION`s you've declared can also be accessed from blueprint on your subsystem:

{{ img(path="scripted-subsystem.png") }}

## Local Player Subsystems

In case of local player subsystems, you need to pass which `ULocalPlayer` to retrieve the subsystem for into the `::Get()` function:

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">UMyPlayerSubsystem</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">UScriptLocalPlayerSubsystem</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">}</span></div><br><div><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">UseScriptedPlayerSubsystem</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">ULocalPlayer</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">RelevantPlayer</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">Gameplay</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">GetPlayerController</span><span style="color: #d4d4d4;">(</span><span style="color: #b5cea8;">0</span><span style="color: #d4d4d4;">).</span><span style="color: #9cdcfe;">LocalPlayer</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">auto</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">MySubsystem</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">UMyPlayerSubsystem</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">Get</span><span style="color: #d4d4d4;">(</span><span style="color: #9cdcfe;">RelevantPlayer</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

> **Note:** It is also possible to directly pass an `APlayerController` when retrieving a local player subsystem.
