

```cpp
/*
 * Template for file structuring, aims to reduce cognitive load.
 * Make concise, discriptive comment for every declarations, unless the name is enough self-explanatory.
 * Log important state's change so it helps announcing unwanted behaviours.
 * Make toggles for drawing important actions and queries so it helps visualising eviromental interactions.
 * Do not use Namespace; always prefer BP accessable Config variables.
 * 
 * Additional Suggestion: 
 * always prefer composition over inheritance, unless inheritance is required, or very benifitial.
 */


/*
 * .h file
 */


#include "CoreMinimal.h"


/* ==================== Declares ==================== */

constexpr float DataFallback = 1.f;


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
 * Functions:
 * - [Discrptions of mains]
 *
 * Rules:
 * - [Definitions of mains]
 *
 * Workflow:
 * - [Descriptions of mains]
 *
 * States:
 * - [Discrptions of mains]
 *
 * Boundary/Limitation:
 * - [Discrptions of mains]
 *
 * Networking:
 * - [mention replcation mode and special networkings]
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
	
	UExampleInherited();
	
	
	/* ==================== Overrides ==================== */
public:
	virtual void BeginPlay() override;
	virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;
	
	

	
	/* ==================== Components ==================== */
protected:
	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, meta = (AllowPrivateAccess = "true"))
	UCameraComponent* FollowCamera;
	
	
public:
	/* ==================== APIs ==================== */
	
	/* ----- Subsection Name01 ----- */
	
	UFUNCTION(BlueprintCallable, Category="Example")
	void Request_StartEntryPoint();
	
	
	
	/* ==================== Queries ==================== */
	
	UFUNCTION(BlueprintPure, Category="Example")
	bool IsActive() const { return bActive; }
	
	
	
	/* ==================== Event Delegates ==================== */
	
	UPROPERTY(BlueprintAssignable, Category="Example")
	FExampleDelegate OnExample;
	
	
	
	/* ==================== Subclasses Extension ==================== */
	
protected:
	virtual void HandleStart();
	virtual void HandleStop();
	
	
	
	/* ==================== Internal Function ==================== */
	
protected:  
    UFUNCTION()  
    void OnRep_CurrentStamina();
	
private:
	/* ----- Subsection Name01 ----- */
	
	// Internal request reroute
	UFUNCTION(Server, Reliable)
	void RpcServer_StartEntryPoint();
	
	// Authrized entrypoint
	bool Auth_TryStart();
	
	
	/* ----- Subsection Name02 ----- */
	
	void DoInternal();
	
	
	/* ----- Subsection Name02 ----- */
	
	void GetOwnerState();
	
	
	
	/* ==================== Runtime State ==================== */
	
	UPROPERTY(Transient, Replicated)
	bool bActive = false;
	
	// internal cached pointers/state (usually not UPROPERTY unless needed for GC/replication)
	TWeakObjectPtr<UPrimitiveComponent> CachedComp;
	
	
	
	/* ==================== Config ==================== */
	
	/* ----- Subsection Name01 ----- */
	
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category="Example|Config", meta=(AllowPrivateAccess="true", ClampMin="0.0"))
	float PrivateData = 100.f;
	
	
	/* ----- Subsection Name02 ----- */
	
	UPROPERTY(EditAnywhere, BlueprintReadWrite, meta=(AllowPrivateAccess="true"))
	TObjectPtr<UExampleClass> ExampleObj;
	
	/* ----- Subsection Name02 ----- */
	
	    UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category="CustomMovement|Climbing|Debug", meta=(AllowPrivateAccess="true"))
    bool bSectionName_DebugDraw = false;
}


/*
 * .cpp file follows the same commented Structure.
 */

```
