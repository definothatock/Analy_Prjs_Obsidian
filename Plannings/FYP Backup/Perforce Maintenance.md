
> Discord record.
 
 tefaeron phinloav [BRUH],  _—_ 12/10/2025 18:20
============================== changelist tags: ===================================
**You can Have Multiple tags in one submit.** But if the changes are distinct, it is suggested to have separate changelists and submissions. 

**PULL Main: **[optional description]
- You get new things from Main stream.
- You fetched ||(taken the updates into your local changelist, but not merged onto server depot)|| and merged ||(applied the changes onto the server depot)|| from a different stream.

**PUSH Main: **[description]
- You push your work to the Main Stream.

**ADD:** [description]
- You added new content(s)-- C++ classes, Systems, Features.

**DEV:** [description]
- Your development on existing content(s).

**ISSUE:** [description]
- There are know issues, but you decided to submit anyways (non-critical)

**BUGFIX:** [description]
- You fixed some known Issues.

**DEL:** [description]
-  You are going to delete some files on the server depot.

**IMPORT:** [content]
- you imported 3rd party content that is already-baked/ready-to-be-used.

**REVERT ** [current-stream] to [revision] **:**  [reason]
- for some reason you need the *server depot* to rollback to a revision. 

**SYNC:** [description]
- you encountered unexpected issue with revision(s) on *server depot*, attempt to sync-revisions/resolve-conflicts.
- supposedly this should not introduce changes outside of the revisions.

**MISC:**  [description]
- for ***rare*** situation that non of the existing tags suit your need.

**TEST:** [description]
- this is reserved only for testing P4 functionalities. 


***Example for a submission with mixed tags:***
Dev: improving the NPC_123 AI logic ;; Issue: AI does not forget after 10s
//
//
------OPTIONALs:------
//

~~These ***greatly improves readability***, but doesn't change the context.

**simplifying **default **Merge **metadata:
Merge: [upper-stream] to [lower-stream]
e.g.:
*Merging //streamsDepot_UEpjMain/UEpjMain to Danny_development (//streamsDepot_UEpjMain/Danny_development) *
simplifies to
Merge: UEpjMain to Danny_development

**simplifying **default **Copy **metadata:
Copy:  [lower-stream] to [upper-stream]
e.g.:
Copying //streamsDepot_UEpjMain/Danny_development to UEpjMain (//streamsDepot_UEpjMain/UEpjMain)
simplifies to
Copy: Danny_development to UEpjMain~~

UPDATE: Just use **PUSH** and **PULL**. The above still has so much unnecessary info.