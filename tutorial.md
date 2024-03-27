Health Monitor - Dashboard
======================
In this activity, you will combine the data from all the topics and display them on the table.


<img src= "https://s3.amazonaws.com/media-p.slid.es/uploads/1525749/images/11199889/pasted-from-clipboard.png" width = "100%" height = "50%">


Follow the given steps to complete this activity.


1. Add the MQTT topic `/heartRate` and connect it to the gauge displaying the heart rate.
* Connect it to the join as well.


2. Double click on the AddToArray function, replace the program with the below program.
   ~~~js
    var tableData = flow.get("savedData") || []


    msg.payload["timeStamp"] = new Date().toLocaleString()


    // Add sugar to payload by formula Blood Glucose Level=0.5×Heart Rate+0.5×SpO2+0.2×Temperature
    msg.payload["sugar"] = 0.5*msg.payload["/heartRate"]
                            + 0.5*msg.payload["/heartRate"]
                            +0.2*msg.payload["/tempValue"]
    // Unshift msg.payload to tableData
    tableData.unshift( msg.payload)
    // set msg.payload as tableData
    msg.payload = tableData


    flow.set("savedData", tableData)


    return msg;
   ~~~
3. Add a column for timestamps and a column for MQTT topics which are not present. Set the size of the table to `20X6`.


<img src= "https://s3.amazonaws.com/media-p.slid.es/uploads/1525749/images/11158525/SA2_Add_Columns.gif" width = "50%" height = "50%">


* Save and run the code to check the output.
