

```cpp
/*
 * Template for file structuring. 
 * Make comment for every declarations, unless the name is enough self-explanatory.
 */


/*
 * .h file
 */

#include "CoreMinimal.h"

// ==================== Declares ====================

USTRUCT()  
struct ExampleStruct  
{  
    GENERATED_BODY()  
  
    UPROPERTY()  
    FName ExampleId = NAME_None;  
};


DECLARE_DYNAMIC_MULTICAST_DELEGATE(FExampleDelegate);



/*
 * [discription of the main purpose]
 *
 * Main Functions:
 * - [Discrptions]
 *
 * Main Rules:
 * - [definitions]
 * 
 * States:
 * - [Discrptions]
 *
 * Boundary:
 * - [Discrptions]
 *
 * Networking:
 * - [mention replcation mode and special neworkings]
 *
 * Reference:
 * - [mention if exists]
 *
 * Future Works:
 * - [Mention what will be added/changed, if planned]
 *
 * Notice:
 * - [Specific things to mention, if any]
 *
 */
UCLASS(ClassGroup=(Custom), meta=(BlueprintSpawnableComponent))  
class EXAMPLE_API UExampleInherited : public UExampleParent 
{  
    GENERATED_BODY()
public:
	UExampleInherited();
	
	
protected:
	
	/* ==================== Overrides ==================== */
	
	virtual void BeginPlay() override;
	virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;
	
	
public:
	
	/* ==================== APIs ==================== */
	
	UFUNCTION(BlueprintCallable, Category="Example")
	void Request_Start();
	
	
	/* ==================== Queries ==================== */
	
	UFUNCTION(BlueprintPure, Category="Example")
	bool IsActive() const { return bActive; }
	
	
	/* ==================== Delegates ==================== */
	
	UPROPERTY(BlueprintAssignable, Category="Example")
	FExampleDelegate OnExample;
	
	
protected:
	
	/* ==================== Subclasses Extension ==================== */
	
	virtual void HandleStart();
	virtual void HandleStop();
	
	
private:
	
	/* ==================== Internal Function ==================== */
	
	/* ----- Subsection Name01 ----- */
	
	// Internal request reroute
	UFUNCTION(Server, Reliable)
	void RpcServer_Start();
	
	// ServerSide works
	bool Auth_TryStart();
	
	/* ----- Subsection Name02 ----- */
	
	void DoInternal();
	
	/* ==================== Runtime State ==================== */
	
	UPROPERTY(Transient, Replicated)
	bool bActive = false;
	
	// internal cached pointers/state (usually not UPROPERTY unless needed for GC/replication)
	TWeakObjectPtr<UPrimitiveComponent> CachedComp;
	
	
	/* ==================== Config ==================== */
	
	// Editor Blueprints can read/tweak, no external change.
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category="Example|Config", meta=(AllowPrivateAccess="true", ClampMin="0.0"))
	float PrivateData = 100.f;
	
	
	/* ==================== Helpers ==================== */
	
	void GetOwnerState();
	
}


/*
 * .cpp file follows the same Structure.
 */

```