trigger leasetrackingtrigger on Lease_Tracking__c (After insert,After update) {

    

       if(Trigger.isAfter && Trigger.IsUpdate)

    {

        LeaseTrackingTriggerHandler.method1(trigger.old);

    }

## Create an apex class and Name it LeaseTrackingTriggerHandler
public class LeaseTrackingTriggerHandler {

    

     public static void method1(List<Lease_Tracking__c> lt1)

   {

       for(Lease_Tracking__c lt2: lt1 )

       {

           if(lt2.Amount_to_be_paid__c > (lt2.Total_rent_Yearly__c)/2)

           {

               Messaging.SingleEmailMessage M = New Messaging.SingleEmailMessage();

               

                List<String> ToADD = New List<String>{lt2.Email_id__c};

                    

                      M.setToAddresses(ToADD);

                      M.setSubject('Regarding the Pending Rent'); 

                      M.setPlainTextBody('Hello, This is an Reminder for you to complete your due rent by the end this month, your due rent thatneeds to be paid is' +lt2.Amount_to_be_paid__c); 

               

               

               

                    List<Messaging.Email> AB = New List<Messaging.Email>{};

                    AB.add(M);

                    Messaging.sendEmail(AB);

        

        

             

        

           }

       }

   }
