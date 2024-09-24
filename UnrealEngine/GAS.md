
FGameplayAbilityActorInfo
+ OwnerActor 可以是 PlayerState RTS游戏
+ AvatarActor 





GameplayEffect

Instant 即时伤害之类

Infinite 无持续时间，流血之类，
    period每间隔多少秒应用一次，流血类，持续恢复类
    Execute Periodic Effect on Application(bExecutePeriodicEffectOnApplication) 下一帧会立即执行一次
    inhibited 可以抑制

hasDuration buff有持续时间

Modifier简单计算
Executions自定义计算
所以当我们明确知道需要修改哪个属性，并且一次计算只会修改一个Attribute，则使用Modifiers更好。若无法明确知道修改哪个属性，需要在运行时根据状态动态决定，并且可能需要修改多个Attribute时，则需要使用Executions


Stacking仅适用于持续性Effect中（Has Duration, Infinite）

GameplayEffectComponents
    ChanceToApply
    CustomCanApply
    BlockAbilityTags
    TargetTagRequirements
    TargetTags




AttributeSet

PreGameplayEffectExecute -> 
PreAttributeBaseChange -> 
PostAttributeBaseChange -> 
PostGameplayEffectExecute


