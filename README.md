## Welcome to Game Booster Docs

**Game Booster** is a set of scripts to create your game. It has a lot of daily common logic to accelerate your development. There is components to deal with movement, instantiation, destruction, input, score, and lot more.

The main principle of **Game Booster** is reusability. To achieve this, each component do simple things, and can be connected with others components (even your scripts) to achieve more complex behaviours. Many scripts has UnityEvent fields, which allows you to connect some event with other object’s methods and attributes on your scene.

The components> are splitted in several categories: Basics, Movement, Physics, Collision Detection, Input, Time, Vars, Score, Mechanics and Audio.

- [Basics components](#basics-components)
  - [BehaviourEvents](#behaviourevents)
  - [Creator](#creator)
  - [Destroyer](#destroyer)
  - [ObjectSelector](#objectselector)
  - [SceneMethods](#scenemethods)
  - [TransformMethods](#transformmethods)
- [Input components](#input-components)
  - [AxisInput](#axisinput)
  - [KeyInput](#keyinput)
  - [MousePositionInput](#mousepositioninput)
- [Movement components](#movement-components)
  - [AngularVelocity2D](#angularvelocity2d)
  - [AngularVelocity3D](#angularvelocity3d)
  - [FollowScreenPosition2D](#followscreenposition2d)
  - [FollowTarget2D](#followtarget2d)
  - [FollowTarget3D](#followtarget3d)
  - [LookToTarget2D](#lookTotarget2d)
  - [Velocity2D](#velocity2d)
  - [Velocity3D](#velocity3d)
- [Physics components](#physics-components)
  - [Ridigbody2DMethods](#ridigbody2dmethods)
  - [RidigbodyMethods](#ridigbodymethods)
  - [SpeedLimit2D](#speedlimit2d)
  - [SpeedLimit3D](#speedlimit3d)
- [Collision Detection components](#collision-detection-components)
  - [CollisionDetector2D](#collisiondetector2d)
  - [CollisionDetector3D](#collisiondetector3d)
- [Time components](#time-components)
  - [TimedActions](#timedactions)
  - [TimedActionSequence](#timedactionsequence)
  - [Timer](#timer)
- [Vars components](#vars-components)
  - [IntVar](#intvar)
  - [IntVarRef](#intvarref)
  - [FloatVar](#floatvar)
  - [FloatVarRef](#floatvarref)
  - [BoolVar](#boolvar)
  - [BoolVarRef](#boolvarref)
- [Score components](#score-components)
  - [Score](#score)
  - [ScoreMaker](#scoremaker)
- [Mechanics components](#mechanics-components)
  - [MoveFourDirections2D](#movefourdirections2d)
  - [Platform2D](#platform2d)
  - [Tank2D](#tank2d)
- [Audio components](#audio-components)
  - [AudioManager](#audiomanager)
  - [AudioManagerControl](#audiomanagercontrol)

## Basics components

Basics components deal with fundamental logic in Game Booster

### BehaviourEvents

![Image](images/BehaviourEvents.png)

Creates events for each MonoBehaviour events like Awake, Start, Update, OnEnable, etc. This component helps you to put simple logic in some MonoBehaviour event without creating a new script to it.

Fields:
- `Enum eventType` : Enum of each event will be received
- `UnityEvent actions` : Events that will be called when the event set in EventType happens

### Creator

![Image](images/Creator.png)

Creates instance of prefabs. Randomically choose one prefab from the list to be instantiated at some spawn point.

Fields:
- `List<GameObject> prefabs` : Prefabs to be instantiated (random choosen).
- `bool useRotation` : Use spawn point rotation as rotation of the instantiated object
- `bool insideHierarchy` : Place the instantiated object inside other object's hierarchy
  - `Transform parent` : Object to put the instantiated objects
- `bool useSpawnPoints` : Use other spawn points instead of this object
  - `List<Transform> spawnPoints` : Spawn points where the prefab will be instantiated (random choosen)
- `bool autoCreate` : Automatically instantiate
  - `float startTime` : Time to start prefab instantiation
  - `float repeatTime` : Time between instantiations

Methods:
- `void Create()` : Instantiate a prefab using the options set

### Destroyer

![Image](images/Destroyer.png)

This component has a few ways to destroy the object it is attached to.

Fields:
- `float selfDestructionTime` : Time to self destruction. Set 0(zero) to disable.
- `float timeToDestroy` : Time to destroy when 'DestroyThis' method is called
- `GameObject explosionPrefab` : Prefab to replace the destroyed object

Methods:
- `void DestroyThis()` : destroy this object including all options set
- `void DestroyThisNow()` : destroy this object ignoring timeToDestroy option
- `void DestroyThisWithoutExplosion()` : destroy this object ignoring explosion
- `void JustDestroyThis()` : destroy this object ignoring all options

### ObjectSelector

![Image](images/ObjectSelector.png)

Selects one object of a list, activating it, and deactivating the others of the list. Can be used to switch between weapons, costumes, screens, etc.

Fields:
- `GameObject startSelected` : Selected object at start
- `bool autoSelectOnEnable` : Select the 'startSelected' object on OnEnable event occours
- `List\<GameObject\> objects` : Selectable objects

Methods:
- `void SelectFirst()` : selects the first object of the list
- `void SelectNext()` : selects the next object of the list, after the current selected
- `void SelectPrevious()` : selects the previous object of the list, before the current selected
- `void SelectNone()` : deselects all objects (deactivating all)
- `void Select(GameObject obj)` : selects the object passed as parameter
- `void Select(string name)` : selects the object of the list with the name passed as parameter
- `void Select(int index)` : selects the object of the list at the position passed as parameter

### SceneMethods

![Image](images/SceneMethods.png)

Gives access to static methods relative to the scene. This component don’t add features, just gives access point to static methods and properties to be called via events by other components.

Methods:
- `void LoadScene(string sceneName)` : load another scene
- `void ReloadCurrentScene()` : reload current scene
- `void ApplicationQuit()` : quit application
- `void Pause()` : set Time.timeScale = 0
- `void Resume()` : set Time.timeScale = 1

### TransformMethods

![Image](images/TransformMethods.png)

Methods and properties to set only one axis of position/scale/rotation and copy position/scale/rotation from other transform.

Properties:
- `float positionX` : set position.x value
- `float positionY` : set position.y value
- `float positionZ` : set position.z value
- `float localPositionX` : set localPosition.x value
- `float localPositionY` : set localPosition.y value
- `float localPositionZ` : set localPosition.z value
- `Vector2 positionXY` : set position.x and position.y values
- `Vector2 localPositionXY` : set localPosition.x and localPosition.y values
- `float localScaleX` : set localScale.x value
- `float localScaleY` : set localScale.y value
- `float localScaleZ` : set localScale.z value
- `float eulerAnglesX` : set eulerAngles.x value
- `float eulerAnglesY` : set eulerAngles.y value
- `float eulerAnglesZ` : set eulerAngles.z value
- `float localEulerAnglesX` : set localEulerAngles.x value
- `float localEulerAnglesY` : set localEulerAngles.y value
- `float localEulerAnglesZ` : set localEulerAngles.z value

Methods:
- `void SetPositionFrom(Transform target)` : copy position from target transform
- `void SetLocalPositionFrom(Transform target)` : copy localPosition from target transform
- `void SetRotationFrom(Transform target)` : copy rotation from target transform
- `void SetLocalRotationFrom(Transform target)` : copy localRotation from target transform
- `void SetLocalScaleFrom(Transform target)` : copy localScale from target transform

## Input components

Components to get player's input.

### AxisInput

![Image](images/AxisInput.png)

Gets axis input value.

Fields:
- `string axisName` : Axis name (ex: "Horizontal", "Vertical" )
- `bool raw` : Get input raw value
- `float multiplier` : Axis will be multiplied by this value
- `UnityEvent<float> actions` : event called at each frame passing axis value

### KeyInput

![Image](images/KeyInput.png)

Gets key input events.

Fields:
- `EventType eventType` : Type of key event
- `KeyCode key` : Key code
- `UnityEvent<bool> actions` : event called when the key event happens

`EventType` enum values:
- `Pressed` : event is called when the key is pressed
- `Released` : event is called when the key is released
- `Repeat` : event is called each update

### MousePositionInput

![Image](images/MousePositionInput.png)

Gets mouse position.

Fields:
- `PositionType positionType` : Mouse position coordinate.
- `UnityEvent<Vector2> actions` : events called each update passing the mouse position

`PositionType` enum values:
- `World2D` : mouse position in the world coordinates using a orthographic camera
- `Screen` : absolute mouse position in the screen
- `Viewport` : mouse position relative to screen from (0,0) at botton left to (1,1) at top right
- `CenteredViewport` : mouse position relative to screen with (0,0) at screen center

## Movement components

Components to control object's movement.

### AngularVelocity2D

![Image](images/AngularVelocity2D.png)

Controls the Rigidbody2D/Transform angular velocity.

Fields:
- `float velocity` : 
- `ControlType controlType` : 

Methods:
- `void ApplyVelocity()` : apply the velocity to the Rigidbody2D/Transform

`ControlType` enum values:
- `Continuous` : angular velocity is continuous set
- `OnStart` : angular velocity is set on `Start` event
- `OnEnable` : angular velocity is set on `OnEnable` event
- `Manual` : angular velocity is set when the method `ApplyVelocity()` is called

### AngularVelocity3D

![Image](images/AngularVelocity3D.png)

Controls the Rigidbody3D/Transform angular velocity.

Fields:
- `Vector3 angularVelocity` : Current angular velocity
- `float angularVelocityX` : Current x angular velocity
- `float angularVelocityY` : Current y angular velocity
- `float angularVelocityZ` : Current z angular velocity
- `ControlType controlType` : How the angular velocity is controled

Methods:
- `void ApplyVelocity()` : apply the velocity to the Rigidbody3D/Transform

`ControlType` enum values:
- `Continuous` : angular velocity is continuous set
- `OnStart` : angular velocity is set on `Start` event
- `OnEnable` : angular velocity is set on `OnEnable` event
- `Manual` : angular velocity is set when the method `ApplyVelocity()` is called

### FollowScreenPosition2D

![Image](images/FollowScreenPosition2D.png)

Follows a position relative to screen.

Fields:
- `ControlType controlType` : How the position is controled
- `Vector2 viewportAnchor` : Screen viewport anchor (from 0.0 to 1.0)
- `Vector2 offset` : Position offset in world coordinates

Methods:
- `void ApplyPosition()` : apply the position relative to screen 

`ControlType` enum values:
- `Continous` : Apply position every frame
- `OnStart` : Apply position on `Start` event
- `OnEnable` : Apply position on `OnEnable` event
- `Manual` : Apply position when the method `ApplyPosition()` is called

### FollowTarget2D

![Image](images/FollowTarget2D.png)

Follows a target position.

Fields:
- `Transform target` : Target that will be followed
- `Vector2 offset` : Position offset from target
- `float speed` : Speed at which the object will move to target. Set 0(zero) to infinity speed.
- `Axis axis` : Axis affected by target position

`Axis` enum values:
- `XY` : affects x and y axis
- `X` : affects x axis
- `Y` : affects y axis

### FollowTarget3D

![Image](images/FollowTarget3D.png)

Follow a target position.

Fields:
- `Transform target` : Target that will be followed
- `Vector3 offset` : Position offset from target
- `float speed` : Speed at which the object will move to target. Set 0(zero) to infinity speed.
- `Axis axis` : Axis affected by target position

`Axis` enum values :
- `XYZ` : affects x, y and x axis
- `XY` : affects x and y axis
- `XZ` : affects x and z axis
- `YZ` : affects y and z axis
- `X` : affects x axis
- `Y` : affects y axis
- `Z` : affects z axis

### LookToTarget2D

![Image](images/LookToTarget2D.png)

Makes the object look (rotate) to some target.

Fields:
- `Transform target` : Target the object will look to.
- `float speed` : Angular speed at which the object will rotate. Set 0(zero) to infinity speed.
- `float angleOffset` : Angle offset to fix object rotation

### Velocity2D

![Image](images/Velocity2D.png)

Controls Rigidbody2D/Transform velocity.

Fields:
- `Vector2 velocity` : Current velocity
- `float velocityX` : Current x velocity
- `float velocityY` : Current y velocity
- `bool local` : Use object local orientation
- `ControlType controlType` : How the velocity is controlled
- `Axis axis` : Axis affected

Methods:
- `void ApplyVelocity()` : Applies current velocity

`ControlType` enum values:
- `Continous` : Apply velocity every frame
- `OnStart` : Apply velocity on `Start` event
- `OnEnable` : Apply velocity on `OnEnable` event
- `Manual` : Apply velocity when the method `ApplyVelocity()` is called

`Axis` enum values:
- `XY` : affects x and y axis
- `X` : affects x axis
- `Y` : affects y axis

### Velocity3D

![Image](images/Velocity3D.png)

Controls Rigidbody3D/Transform velocity.

Fields:
- `Vector3 velocity` : Current velocity
- `float velocityX` : Current x velocity
- `float velocityY` : Current y velocity
- `float velocityZ` : Current z velocity
- `bool local` : Use object local orientation
- `ControlType controlType` : How the velocity is controlled
- `Axis axis` : Axis affected

Methods:
- `void ApplyVelocity()` : Applies current velocity

`ControlType` enum values:
- `Continous` : Apply velocity every frame
- `OnStart` : Apply velocity on `Start` event
- `OnEnable` : Apply velocity on `OnEnable` event
- `Manual` : Apply velocity when the method `ApplyVelocity()` is called

`Axis` enum values :
- `XYZ` : affects x, y and x axis
- `XY` : affects x and y axis
- `XZ` : affects x and z axis
- `YZ` : affects y and z axis
- `X` : affects x axis
- `Y` : affects y axis
- `Z` : affects z axis

## Physics components

Components to control some physics properties.

### Ridigbody2DMethods

![Image](images/Ridigbody2DMethods.png)

Extra methods to control Rigidbody2D.

Fields:
- `float velocityX` : set x velocity
- `float velocityY` : set y velocity

Methods:
- `void InvertVelocity()` : inverts rigidbody velocity (velocity = -velocity)
- `void InvertVelocityX()` : inverts rigidbody x velocity (velocity.x = -velocity.x)
- `void InvertVelocityY()` : inverts rigidbody y velocity (velocity.y = -velocity.y)
- `void InvertAngularVelocity()` : inverts rigidbody angular velocity (angularVelocity = -angularVelocity)
- `void NormalizeVelocity(float speed)` : normalizes rigidbody velocity (velocity = velocity.normalized * speed

### RidigbodyMethods

![Image](images/RidigbodyMethods.png)

Extra methods to control Rigidbody.

Fields:
- `float velocityX` : set x velocity
- `float velocityY` : set y velocity
- `float velocityZ` : set z velocity
- `float angularVelocityX` : set x angular velocity
- `float angularVelocityY` : set y angular velocity
- `float angularVelocityZ` : set z angular velocity

Methods:
- `void InvertVelocity()` : inverts rigidbody velocity (velocity = -velocity)
- `void InvertVelocityX()` : inverts rigidbody x velocity (velocity.x = -velocity.x)
- `void InvertVelocityY()` : inverts rigidbody y velocity (velocity.y = -velocity.y)
- `void InvertVelocityZ()` : inverts rigidbody z velocity (velocity.z = -velocity.z)
- `void InvertAngularVelocityX()` : inverts rigidbody angular velocity x (angularVelocity.x = -angularVelocity.x)
- `void InvertAngularVelocityY()` : inverts rigidbody angular velocity y (angularVelocity.y = -angularVelocity.y)
- `void InvertAngularVelocityZ()` : inverts rigidbody angular velocity z (angularVelocity.z = -angularVelocity.z)
- `void NormalizeVelocity(float speed)` : normalizes rigidbody velocity (velocity = velocity.normalized * speed
- `void NormalizeVelocityXY(float speed)()` : normalizes rigidbody velocity xy
- `void NormalizeVelocityXZ(float speed)()` : normalizes rigidbody velocity xz
- `void NormalizeVelocityYZ(float speed)()` : normalizes rigidbody velocity yz

### SpeedLimit2D

![Image](images/SpeedLimit2D.png)

Limits the rididbody speed below a value.

Fields:
- `float maxSpeed` : Maximum speed allowed

### SpeedLimit3D

![Image](images/SpeedLimit3D.png)

Limits the rididbody speed below a value.

Fields:
- `float maxSpeed` : Maximum speed allowed

## Collision Detection components

### CollisionDetector2D

![Image](images/CollisionDetector2D.png)

Detects 2D collisions.

Fields:
- `CollisionEvent collisionEvent` : Collision event
- `CollisionType collisionType` : Collider type
- `string tags` : Tags to filter collision. Use ';' to separate more tags.
- `UnityEvent<GameObject> actions` : Event called when a collision occurs

`CollisionEvent` enum values:
- `Enter` : When this rigidbody/collider has begun touching another rigidbody/collider
- `Exit` : When this rigidbody/collider has stopped touching another rigidbody/collider
- `Stay` : Once per frame for every collider/rigidbody that is touching rigidbody/collider

`CollisionType` enum values:
- `Any` : Collision and Trigger events
- `Collision` : Only collision events (non trigger)
- `Trigger` : Only trigger events

### CollisionDetector3D

![Image](images/CollisionDetector3D.png)

Detects 3D collisions.

Fields:
- `CollisionEvent collisionEvent` : Collision event
- `CollisionType collisionType` : Collider type
- `string tags` : Tags to filter collision. Use ';' to separate more tags.
- `UnityEvent<GameObject> actions` : Event called when a collision occurs

`CollisionEvent` enum values:
- `Enter` : When this rigidbody/collider has begun touching another rigidbody/collider
- `Exit` : When this rigidbody/collider has stopped touching another rigidbody/collider
- `Stay` : Once per frame for every collider/rigidbody that is touching rigidbody/collider

`CollisionType` enum values:
- `Any` : Collision and Trigger events
- `Collision` : Only collision events (non trigger)
- `Trigger` : Only trigger events

## Time components

Components to deal with actions over time.

### TimedActions

![Image](images/TimedActions.png)

Executes actions repeatedly over time.

Fields:
- `float startTime` : Time to wait before the first execution starts
- `float repeatTime` : Time between two executions
- `UnityEvent actions` : Events called

### TimedActionSequence

![Image](images/TimedActionSequence.png)

Executes a sequence of actions with time between them.

Fields:
- `TimedAction[] actions` : Actions to be executed
  - `TimedAction` :
    - `float waitTime` : Time to wait before execute
    - `UnityEvent actions` : Actions to execute
- `ControlType controlType` : How actions are executed
- `bool continuous` : Continuous execute actions

Methods:
- `void CallActions()` : Start execute actions

`ControlType` enum values:
- `OnStart` : Executes when `Start` event occurs
- `OnEnable` : Executes when `OnEnable` event occurs
- `Manual` : Executes when method `CallActions` is called

### Timer

![Image](images/Timer.png)

A timer (clock).

Fields:
- `float currentTime` : Current time (seconds)
- `float startTime` : Initial time
- `bool countdown` : If the timer is countdown
- `float minValue` : Minimum timer value
- `float maxvalue` : Maximum timer value
- `bool paused` : If the timer is paused
- `TimerEvents events` : Timer events
  - `UnityEvent<float> onChange` : Event called when the timer value changes
  - `UnityEvent<float> onMinValue` : Event called when the timer reaches the min value
  - `UnityEvent<float> onMaxValue` : Event called when the timer reaches the max value
  - `int textDigits` : Digits to show at the OnChangeText event
  - `UnityEvent<string> onChangeText` : Event called when the timer value changes, passing its conversion to string

Methods:
- `void AddTime(float time)` : Adds some time to currentTime
- `void Pause()` : Pause the clock
- `void Resume()` : Resume the clock
- `void SwitchPause()` : Swith between Paused and Resumed clock

## Vars components

Components to store variables inside components.

### IntVar

![Image](images/IntVar.png)

Stores a global int variable.

Fields:
- `string id` : variable identifier
- `int value` : current value
- `int startValue` : start variable value
- `FilterType filter` : Filter to apply when value changes
- `bool limitValue` : limit variable value
  - `int minValue` : min value allowed
  - `int maxValue` : max value allowed
- `bool storeOnPlayerPrefs` : store this variable in PlayerPrefs
  - `string playerPrefsKey` : PlayerPrefs key
  - `bool autoLoadOnStart` : auto load variable from PlayerPrefs
  - `bool autoSave` : auto save variable in PlayerPrefs

Methods:
- `void Add(int inc)` : Adds this variable to some value (value += inc)
- `void Multiply(int multiplier)` : Multiply this variable by some value (value *= multiplier)
- `void Divide(int divider)` : Divide this variable by some value (value /= divider)
- `void SetValue(int value)` : Change this variable value
- `void ResetValue()` : Reset value to `startValue`
- `void SaveOnPlayerPrefs()` : Save on PlayerPrefs
- `void LoadFromPlayerPrefs()` : Load from PlayerPrefs

`FilterType` enum values:
- `None` : No filter
- `KeepMinValue` : Keep minimum value when value changes
- `KeepMaxValue` : keep maximum value when value changes

### IntVarRef

![Image](images/IntVarRef.png)

Reference to a [IntVar](#intvar) component.

Fields:
- `string varId` : Referenced `IntVar` identifier
- `GlobalVariablePlace varPlace` : Referenced `IntVar` search place
- `GlobalVarGetEvents<int> getValue` : Ways to get referenced `IntVar` value
  - `bool condition` : submit the `getValue` to some condition
    - `bool ignoreConditionOnStart` : ignore this condition on first value get
    - `GlobalVarComparisonType comparison` : condition comparison
    - `int comparisonValue` : condition comparison value
  - `UnityEvent<int> onValueChange` : event called when the value changes
  - `UnityEvent<string> onValueChangeText` : event called when the value changes passing its conversion to string

Methods:
- `void Add(int inc)` : Adds the referenced variable to some value (value += inc)
- `void Multiply(int multiplier)` : Multiply the referenced variable by some value (value *= multiplier)
- `void Divide(int divider)` : Divide the referenced variable by some value (value /= divider)
- `void SetValue(int value)` : Change the referenced variable value
- `void ResetValue()` : Reset the referenced variable value to `startValue`
- `void SaveOnPlayerPrefs()` : Save the referenced variable on PlayerPrefs
- `void LoadFromPlayerPrefs()` : Load the referenced variable from PlayerPrefs

`GlobalVariablePlace` enum values:
- `Anywhere` : Find the `IntVar` anywhere in the scene
- `Self` : Find the `IntVar` in its own `GameObject`
- `Children` : Find the `IntVar` in this object's children
- `Parent` : Find the `IntVar` in this object's parents

`GlobalVarComparisonType` enum values:
- `Equals` : if the variable value is equals to the `comparisonValue`
- `NotEquals` : if the variable value is not equals to the `comparisonValue`
- `LessThan` : if the variable value is less than the `comparisonValue`
- `LessOrEqualTo` : if the variable value is less or equal to the `comparisonValue`
- `GreaterThan` : if the variable value is greater than the `comparisonValue`
- `GreaterOrEqualTo` : if the variable value is greater or equal to the `comparisonValue`

### FloatVar

![Image](images/FloatVar.png)

Stores a global float variable.

Fields:
- `string id` : variable identifier
- `float value` : current value
- `float startValue` : start variable value
- `FilterType filter` : Filter to apply when value changes
- `bool limitValue` : limit variable value
  - `float minValue` : min value allowed
  - `float maxValue` : max value allowed
- `bool storeOnPlayerPrefs` : store this variable in PlayerPrefs
  - `string playerPrefsKey` : PlayerPrefs key
  - `bool autoLoadOnStart` : auto load variable from PlayerPrefs
  - `bool autoSave` : auto save variable in PlayerPrefs

Methods:
- `void Add(float inc)` : Adds this variable to some value (value += inc)
- `void Multiply(float multiplier)` : Multiply this variable by some value (value *= multiplier)
- `void Divide(float divider)` : Divide this variable by some value (value /= divider)
- `void SetValue(float value)` : Change this variable value
- `void ResetValue()` : Reset value to `startValue`
- `void SaveOnPlayerPrefs()` : Save on PlayerPrefs
- `void LoadFromPlayerPrefs()` : Load from PlayerPrefs

`FilterType` enum values:
- `None` : No filter
- `KeepMinValue` : Keep minimum value when value changes
- `KeepMaxValue` : keep maximum value when value changes

### FloatVarRef

![Image](images/FloatVarRef.png)

Reference to a [FloatVar](#floatvar) component.

Fields:
- `string varId` : Referenced `FloatVar` identifier
- `GlobalVariablePlace varPlace` : Referenced `FloatVar` search place
- `GlobalVarGetEvents<float> getValue` : Ways to get referenced `FloatVar` value
  - `bool condition` : submit the `getValue` to some condition
    - `bool ignoreConditionOnStart` : ignore this condition on first value get
    - `GlobalVarComparisonType comparison` : condition comparison
    - `float comparisonValue` : condition comparison value
  - `UnityEvent<float> onValueChange` : event called when the value changes
  - `UnityEvent<string> onValueChangeText` : event called when the value changes passing its conversion to string

Methods:
- `void Add(float inc)` : Adds the referenced variable to some value (value += inc)
- `void Multiply(float multiplier)` : Multiply the referenced variable by some value (value *= multiplier)
- `void Divide(float divider)` : Divide the referenced variable by some value (value /= divider)
- `void SetValue(float value)` : Change the referenced variable value
- `void ResetValue()` : Reset the referenced variable value to `startValue`
- `void SaveOnPlayerPrefs()` : Save the referenced variable on PlayerPrefs
- `void LoadFromPlayerPrefs()` : Load the referenced variable from PlayerPrefs

`GlobalVariablePlace` enum values:
- `Anywhere` : Find the `FloatVar` anywhere in the scene
- `Self` : Find the `FloatVar` in its own `GameObject`
- `Children` : Find the `FloatVar` in this object's children
- `Parent` : Find the `FloatVar` in this object's parents

`GlobalVarComparisonType` enum values:
- `Equals` : if the variable value is equals to the `comparisonValue`
- `NotEquals` : if the variable value is not equals to the `comparisonValue`
- `LessThan` : if the variable value is less than the `comparisonValue`
- `LessOrEqualTo` : if the variable value is less or equal to the `comparisonValue`
- `GreaterThan` : if the variable value is greater than the `comparisonValue`
- `GreaterOrEqualTo` : if the variable value is greater or equal to the `comparisonValue`

### BoolVar

![Image](images/BoolVar.png)

Stores a global bool variable.

Fields:
- `string id` : variable identifier
- `bool value` : current value
- `bool startValue` : start variable value
- `bool storeOnPlayerPrefs` : store this variable in PlayerPrefs (as an int 0 or 1)
  - `string playerPrefsKey` : PlayerPrefs key
  - `bool autoLoadOnStart` : auto load variable from PlayerPrefs
  - `bool autoSave` : auto save variable in PlayerPrefs

Methods:
- `void Or(bool value)` : Applies an 'or' operator with some value (varValue = varValue || value)
- `void And(bool value)` : Applies an 'and' operator with some value (varValue = varValue && value)
- `void Neg()` : Inverts the value (varValue = !varValue)
- `void SetValue(int value)` : Change this variable value
- `void ResetValue()` : Reset value to `startValue`
- `void SaveOnPlayerPrefs()` : Save on PlayerPrefs
- `void LoadFromPlayerPrefs()` : Load from PlayerPrefs

### BoolVarRef

![Image](images/BoolVarRef.png)

Reference to a [BoolVar](#boolvar) component.

Fields:
- `string varId` : Referenced `BoolVar` identifier
- `GlobalVariablePlace varPlace` : Referenced `BoolVar` search place
- `GlobalVarGetEvents<bool> getValue` : Ways to get referenced `BoolVar` value
  - `bool condition` : submit the `getValue` to some condition
    - `bool ignoreConditionOnStart` : ignore this condition on first value get
    - `GlobalVarComparisonType comparison` : condition comparison
    - `bool comparisonValue` : condition comparison value
  - `UnityEvent<bool> onValueChange` : event called when the value changes
  - `UnityEvent<string> onValueChangeText` : event called when the value changes passing its conversion to string

Methods:
- `void Or(bool value)` : Applies an 'or' operator with some value (varValue = varValue || value)
- `void And(bool value)` : Applies an 'and' operator with some value (varValue = varValue && value)
- `void Neg()` : Inverts the value (varValue = !varValue)
- `void SetValue(int value)` : Change this referenced variable value
- `void ResetValue()` : Reset the referenced variable value to `startValue`
- `void SaveOnPlayerPrefs()` : Save the referenced variable on PlayerPrefs
- `void LoadFromPlayerPrefs()` : Load the referenced variable from PlayerPrefs

`GlobalVariablePlace` enum values:
- `Anywhere` : Find the `BoolVar` anywhere in the scene
- `Self` : Find the `BoolVar` in its own `GameObject`
- `Children` : Find the `BoolVar` in this object's children
- `Parent` : Find the `BoolVar` in this object's parents

`GlobalVarComparisonType` enum values:
- `Equals` : if the variable value is equals to the `comparisonValue`
- `NotEquals` : if the variable value is not equals to the `comparisonValue`
- `LessThan` : if the variable value is less than the `comparisonValue`
- `LessOrEqualTo` : if the variable value is less or equal to the `comparisonValue`
- `GreaterThan` : if the variable value is greater than the `comparisonValue`
- `GreaterOrEqualTo` : if the variable value is greater or equal to the `comparisonValue`

## Score components

Components to score and change player's score and record.

### Score

![Image](images/Score.png)

Stores player score and record.

Fields:
- `string id` : Score id  to differentiate multiple scores
- `int value` : Current score
- `int recordValue` : Current score record
- `bool saveScore` : If the score should be automatically saved
  - `string valuePlayerPrefsKey` : Score PlayerPrefs's key
- `bool saveRecord` : If the record should be automatically saved
  - `string recordPlayerPrefsKey` : Score PlayerPrefs's key
- `ScoreEvents events` : Events relative to score and record
  - `UnityEvent<int> onScoreChange` : Event called when score changes
  - `UnityEvent<int> onRecordChange` : Event called when record changes
  - `UnityEvent<int> onNewRecord` : Event called when score makes a new record
  - `UnityEvent<string> onScoreChangeText` : Event called when score changes passing its conversion to string
  - `UnityEvent<string> onRecordChangeText` : Event called when record changes passing its conversion to string

Methods:
- `void IncScore()` : Adds 1 to score
- `void AddScore(int scoreChange)` : Add some value to score
- `void ResetScore()` : Reset score value do 0(zero).

### ScoreMaker

![Image](images/ScoreMaker.png)

Adds score to [Score](#score) component.

Fields:
- `string scoreId` : Score component id
- `int scoreChange` : Amount of score to be added

Methods:
- `void ApplyScore()` : add `scoreChange` value to referenced score
- `void AddScore(int scoreChange)` : add some value passed as parameter to referenced score

## Mechanics components

Some simple mechanics.

### MoveFourDirections2D

![Image](images/MoveFourDirections2D.png)

Controls an 2D object in all directions.

Fields:
- `string horizontalAxis` : Horizontal axis name
- `string verticalAxis` : Vertical axis name
- `float speed` : Normalized speed

### Platform2D

![Image](images/Platform2D.png)

Simple Platform character physics control.

Fields:
- `float walkInput` : Controls walk direction (-1 to walk left, 0 to stop, +1 to walk right)
- `float walkSpeed` : Speed the character walks
- `float jumpSpeed` : Speed set to y axis when character jumps
- `GroundCheckConfig groundCheckConfig` : Ground check options
  - `LayerMask platformLayers` : Physics Layers to check if character is toutching ground
  - `float width` : raycast width
  - `float height` : raycast height
  - `int rays` : Number of raycasts
- `PlatformEvents events` : events related to platform character
  - `UnityEvent onJump` : Event called when the character jumps
  - `UnityEvent onLand` : Event called when the character fall on ground
  - `UnityEvent onMoving` : Event called when the character starts move
  - `UnityEvent onStop` : Event called when the character stops move
  - `UnityEvent onAir` : Event called when the character go on air without jumping (like falling from a platform)
- `bool defaultInput` : Use default input (keyboard arrows)
  - `string horizontalAxis` : Horizontal axis name
  - `KeyCode jumpKey` : Jump key

Methods:
- `void Jump()` : jump if character is on ground

### Tank2D

![Image](images/Tank2D.png)

Simple Tank physics control (walk forward and rotate).

Fields:
- `float turnInput` : Controls Tank turn direction (-1 to turn left, 0 to stop, +1 to turn right)
- `float moveInput` : Controls Tank move direction (-1 to move backward, 0 to stop, +1 to move forward)
- `float moveSpeed` : speed of Tank movement
- `float turnSpeed` : speed of Tank rotation (in degrees/second)
- `bool onlyTurnIfMoving` : If the Tank can only turn if its moving
- `bool defaultInput` : If use default input
  - `string horizontalAxis` : Horizontal (turn) axis name
  - `string verticalAxis` : Vertical (move) axis name

## Audio components

Some components do control audio in the scene.

### AudioManager

![Image](images/AudioManager.png)

Manager for many AudioSources. Each AudioSource must be attached to a different ´GameObject´ with the right name set.

Fields:
- `List<AudioSource> audios` : List of AudioSources managed by this object.

Methods:
- `void PlayAudio(string name)` : Play some audiosource with the name passed as parameter
- `void StopAudio(string name)` : Stop some audiosource with the name passed as parameter

### AudioManagerControl

![Image](images/AudioManagerControl.png)

Commands the [AudioManager](#audiomanager) component. This component is useful to control the AudioManager from inside a prefab.

Methods:
- `void PlayAudio(string name)` : Play some audiosource in the `AudioManager` with the name passed as parameter
- `void StopAudio(string name)` : Stop some audiosource in the `AudioManager` with the name passed as parameter

