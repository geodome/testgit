# testgit

This is the master branch


# Motion Checklist
* [ ] Motion for Closure of the Debate
* [ ] Motion to Table the Debate
* [ ] Motion for Adjournment of the Meeting
* [ ] Motion for Suspension of the Meeting
* [ ]  Motion to Resume Debate
* [ ] Motion to Introduce an Amendment
* [ ] Motion to Introduce a Working Paper
* [x] Motion for Un-moderated Caucus (its Extension has precedence)    
* [x] Motion for Moderated Caucus (its Extension has precedence)       
* [x] Motion to Change the Speaking Time                              
* [x] Motion to Open the Speaker´s List                               

In order after the Closure of the Debate:

* [ ] Motion to Reorder Draft Resolutions
* [ ] Motion to Divide the Question
* [ ] Motion for the Roll Call


# State Machine for Model UN Procedural Rule
```mermaid
graph LR;

    subgraph Session
        *Open_Session --> Motion_Set_Agenda --> Open_Floor
        *Resume_Session --> Check_Has_Agenda --Yes--> Open_Floor
        Check_Has_Agenda --No--> Motion_Set_Agenda
    end

    subgraph General Speakers GS and Floor Items
        Open_Floor --> Sort_Items --> Check_Items_Exhuasted
        Check_Items_Exhuasted --Yes--> Check_GS_List_Exhuasted
        Check_Items_Exhuasted --No--> Respond_To_Points --> Vote_Until_A_Motion_Pass
        Vote_Until_A_Motion_Pass --All motions fail--> Check_GS_List_Exhuasted
        Vote_Until_A_Motion_Pass --A motion passes--> Execute_Motion
        Check_GS_List_Exhuasted --Yes--> Intervention_GS_Add_Speaker --Yes--> Next_GS_Speaker --> Open_Floor
        Check_GS_List_Exhuasted --No--> Next_GS_Speaker
        Intervention_GS_Add_Speaker --No--> Motion_Close_Debate
    end

    subgraph Closure of Debate
        Execute_Motion --Closure Of Debate--> Motion_Closure_Of_Debate --> Open_Floor
    end

    subgraph Table the Debate
        Execute_Motion --Table the Debate--> Motion_Table_The_Debate --> Open_Floor
    end


    subgraph Unmoderated Caucus UC
        Execute_Motion --Unmoderated Caucus--> Motion_Unmoderated_Caucus --> Open_Floor
    end

    subgraph Moderated Caucus MC
        Execute_Motion --Moderated Caucus--> Motion_Moderated_Caucus --> Check_MC_Timeup
        Check_MC_Timeup --Yes--> Open_Floor
        Check_MC_Timeup --No--> Check_MC_Speaker_List_Exhuasted
        Check_MC_Speaker_List_Exhuasted --Yes--> Intervention_MC_Add_Speaker --No--> Open_Floor
        Intervention_MC_Add_Speaker --Yes--> Next_MC_Speaker
        Check_MC_Speaker_List_Exhuasted --No--> Next_MC_Speaker
        Next_MC_Speaker --> Check_MC_Timeup
    end

    subgraph Set GS Speaker Time
        Execute_Motion --Set Speaker Time--> Motion_Set_GS_Speaker_Time --> Open_Floor
    end

    subgraph Open GS List
        Execute_Motion --Open GS List--> Motion_Open_GS_List --> Open_Floor
    end

```
