trigger leasetrackingtrigger on Lease_Tracking__c (After insert,After update) {

    

       if(Trigger.isAfter && Trigger.IsUpdate)

    {

        LeaseTrackingTriggerHandler.method1(trigger.old);

    }
