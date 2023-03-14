# Is Change Data Collector complicated

The complexity of Change Data Collector (CDC) can depend on various factors such as the specific tool or technology being used, the complexity of the data being collected, and the level of expertise of the individuals using it.
CDC is a process of identifying and capturing changes made to a database or application and storing those changes in a separate location for further processing or analysis. It involves understanding the data schema and the relationships between different data entities to ensure that the captured changes accurately reflect the state of the database.
While CDC can be a complex process, there are many tools available that make it easier for users to capture and process changes without requiring a deep understanding of the underlying technologies. These tools often provide a graphical user interface and automated workflows that simplify the setup and management of the CDC process.
Overall, the complexity of CDC can vary depending on the specific use case and the tools being used, but with the right tools and expertise, it can be a powerful tool for capturing and analyzing changes in data.

# SQL Server CDC (Change Data Capture) 

is a feature in Microsoft SQL Server that allows you to track and capture changes made to your database. CDC provides a reliable and efficient way to identify and capture changes in tables without having to continuously query the entire table for updates.
CDC works by creating a copy of the changed data in a separate table called a change table. The change table contains columns for the old and new values of the changed data, as well as metadata such as the transaction ID, timestamp, and operation type (insert, update, or delete).
To use CDC, you must first enable it on the database and table you want to track changes for. Once enabled, CDC automatically captures changes to the table and stores them in the change table. You can then use this information for a variety of purposes, such as auditing, data replication, and data integration.
Overall, SQL Server CDC is a powerful feature that can provide significant benefits for tracking and analyzing changes in your database. However, it does require some setup and configuration, and it's important to understand how it works to use it effectively.

# Does it require dba on the team?

Using SQL Server CDC does not necessarily require a dedicated DBA on the team, but having someone with expertise in SQL Server and database administration can be helpful for setting up and configuring CDC, as well as for troubleshooting any issues that may arise.
Enabling CDC involves several steps, such as creating change data capture objects, configuring capture instances, and setting up the necessary permissions and roles. While these tasks can be performed by someone with basic SQL Server knowledge, having a DBA on the team can help ensure that CDC is set up correctly and efficiently, and that any potential issues are addressed quickly.
In addition, a DBA can also help optimize the performance of CDC by monitoring system resources and making adjustments as needed, such as increasing the size of the transaction log or changing the capture interval.
Overall, while it is possible to use SQL Server CDC without a dedicated DBA on the team, having someone with expertise in SQL Server and database administration can be beneficial for setting up and maintaining the feature.

# How to use cdc to send messages to azure message bus?

You can use SQL Server CDC to send messages to Azure Service Bus by setting up a process that reads changes from the change table and sends them as messages to the Azure Service Bus queue or topic.
Here are the basic steps to set up this process:

1. Enable CDC on the SQL Server database and table that you want to track changes for.
1. Create a separate SQL Server Agent job to read changes from the change table and send them as messages to the Azure Service Bus queue or topic. This job can use a stored procedure to read changes from the change table and a service bus client library to send messages to the Azure Service Bus. You can use the Azure Service Bus .NET SDK to interact with the Azure Service Bus.
1. Configure the SQL Server Agent job to run at a specified interval, such as every 5 minutes, to read any new changes from the change table and send them as messages to the Azure Service Bus.
1. Create an Azure Service Bus queue or topic to receive the messages from the SQL Server Agent job.

Note that when sending messages to the Azure Service Bus, you will need to ensure that the messages are formatted correctly for the Azure Service Bus. You may also need to configure the Azure Service Bus to handle large volumes of messages and to set up any necessary security or authentication measures.

Overall, using SQL Server CDC to send messages to Azure Service Bus can be a powerful way to integrate your database with other systems and applications, but it does require some setup and configuration to ensure that the process runs smoothly.

## Does that require top tsql sme?

Setting up SQL Server CDC to send messages to Azure Service Bus does require some expertise in SQL Server T-SQL, as well as familiarity with Azure Service Bus and .NET development. However, it may not necessarily require a top T-SQL SME (subject matter expert).

Basic knowledge of T-SQL and SQL Server CDC is required to enable CDC on the database and table and to create the necessary stored procedures and SQL Server Agent jobs to read changes from the change table. Additionally, you will need knowledge of the Azure Service Bus and .NET development to send messages to the Azure Service Bus queue or topic.

If you have experience with SQL Server and T-SQL, and are familiar with Azure Service Bus and .NET development, you may be able to set up this process yourself with some research and experimentation. However, if you are not familiar with these technologies, or if you encounter issues that you are not sure how to resolve, you may need to consult with a more experienced T-SQL SME or SQL Server DBA for assistance.

Overall, setting up SQL Server CDC to send messages to Azure Service Bus requires some expertise in SQL Server and .NET development, but it may not necessarily require a top T-SQL SME if you have some experience and are willing to do some research and experimentation.

