# 关于虚幻引擎内存管理的一些概念和编程技法

## UObject 与 Non-UObject

+ UObject及其子类的堆对象生命周期由GC管理，程序员可以介入。
+ Non-UObject类的对象生命周期管理完全由程序员掌管。
  + 虚幻推荐使用智能指针来管理，必要的时候手工管理内存是被允许的。
+ 两类对象的生命周期可以混合管理，虚幻提供了相应的方案。



## GC 与 UObject

1. 由 NewObject CreateDefaultSubobject 创建出来的 UObject 对象指针会被自动托管到 GC
2. GC 会在合适的时机检查每个 UObject 对象的可达性（IsUnreachable），如果不可达则将其标记等待清除



> ```cpp
> void UContentBrowserAssetDataSource::OnNewAssetRequested(const FName InPath, TWeakObjectPtr<UClass> InFactoryClass, UContentBrowserDataMenuContext_AddNewMenu::FOnBeginItemCreation InOnBeginItemCreation)
> {
> 	UClass* FactoryClass = InFactoryClass.Get();
> 	if (ensure(!InPath.IsNone()) && ensure(FactoryClass) && ensure(InOnBeginItemCreation.IsBound()))
> 	{
> 		UFactory* NewFactory = NewObject<UFactory>(GetTransientPackage(), FactoryClass);
> 
> 		// This factory may get gc'd as a side effect of various delegates potentially calling CollectGarbage so protect against it from being gc'd out from under us
> 		FGCObjectScopeGuard FactoryGCGuard(NewFactory);
> 
> 		FEditorDelegates::OnConfigureNewAssetProperties.Broadcast(NewFactory);
> 		if (NewFactory->ConfigureProperties())
> 		{
> 			FEditorDelegates::OnNewAssetCreated.Broadcast(NewFactory);
> 
> 			FString DefaultAssetName;
> 			FString PackageNameToUse;
> 			AssetTools->CreateUniqueAssetName(InPath.ToString() / NewFactory->GetDefaultNewAssetName(), FString(), PackageNameToUse, DefaultAssetName);
> 
> 			OnBeginCreateAsset(*DefaultAssetName, InPath, NewFactory->GetSupportedClass(), NewFactory, InOnBeginItemCreation);
> 		}
> 	}
> }
> ```
>
> 