---
layout: post
title:  "Exercise 2 - RAG"
categories: workshop
assets: "images/exercise2"
---

# Exercise 2 - Retrieval Augmented Generation

Now that you are more proficient with using Anypoint Code Builder we will go through creating a more complex scenario that allows us to ask AI questions about a document we have given it access to - this is done via Retrieval Augmented Generation (RAG). There are three steps to this:

1.  Create a knowledge store using Embedding
2.  Add a document to the store
3.  Create a query to ask the LLM model questions (Perform RAG)

Let’s get started..

## Initialize the storage

1.  In your current project, go back to the **api.xml** file and select the `get:\rag\store\init` flow

    ![]({{ page.assets}}/1.png)

1.  Remove the existing connector and add a new component by searching "**Embedding new store**".

    ![]({{ page.assets}}/2.png)

1.  Click on the new components and set the store name to:

    ```mule.home ++ ‘/apps/’ ++ app.name ++ ‘/knowledge-centre.store’```

    Remember to click on the small ***fx*** button

    ![]({{ page.assets}}/3.png)

    In this scenario we are using a hard-coded store name

## Add documents to the storage

1.  Select the `get:\rag\store\add-chunks` flow and remove any connector that might already be present.
2.  Click on the "**+**" button and search for the **Embedding add document to store** operation
3.  After inserting the component click on it and configure it with the following settings:

    |   **Parameter**                                                                                    |  **Value**                                                                                                                                     |
    | :-----------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------:|
    |   **Store Name**                                                                      |   ```mule.home ++ ‘/apps/’ ++ app.name ++ ‘/knowledge-centre.store’```  <br/>   **Note**: click on the “fx” icon to enable DataWeave scripting   |
    |   **Context Path**                                                                    |   ```mule.home ++ ‘/apps/’ ++ app.name ++ ‘/MulesoftTXY.pdf’```  <br/>   **Note**: click on the “fx” icon to enable DataWeave scripting          |
    |   Max Segment size                                                                    |   **100000**                                                                                                                          |
    |   Max Overlap Size                                                                    |   **10000**                                                                                                                           |
    |   File Type (you might need to click on the refresh icon for this option to appear)   |   **any**                                                                                                                             |

    The component configuration should look like the following:

    ![]({{ page.assets}}/4.png)
    

## Add chat capabilities

1.  Select the flow `post:\rag\chat`
2.  Remove any existing component
3.  Click on the "**+**" button and search for the **Embedding get info from store** operation 

    {: .warning}
    Ensure you DO NOT select the **Embedding get info from store (legacy)** operation

4.  Select the operation and once it’s been added to the flow, click on it
5.  Configure the component with the following parameters

    |   **Parameter**           |   **Value**                                                                                                                                                |
    | :-----------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------: |
    |   **Connection Config**   |   MuleChain-Azure-AI-Config                                                                                                                       |
    |   **Data**                |   ```payload.data ++ \". Don't make any assumption\"```                                                                                                   |
    |   **Store Name**          |   ```mule.home ++ '/apps/' ++ app.name ++ '/knowledge-centre.store'```  <br/>   **Note**: Ensure you select the “fx” button to enable DataWeave expression   |
    |   **Get latest**          |   Selected                                                                                                                                        |

    The component configuration should look like the following screenshot:

    ![]({{ page.assets}}/5.png)
    

1.  Click on the "**+**" button below the **Embedding get info** operation to add a new operation and search for the **Chat answer prompt** operation

    {: .note}
    Ensure you select the operation that belongs to the MuleSoft AI Chain connector, not the Einstein AI one as shown in the image below:

    ![]({{ page.assets}}/6.png)

1.  Once added to the flow, add the following parameters:

    |  **Parameter**          |   **Value**                                                                                                   |
    | :-----------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------: |
    |   **Connection Config**   |   MuleChain-Azure-AI-Config                                                                                |
    |   **Prompt**              |   ```"Provide a summary of the following content related to MuleSoft TXY: \n" ++ ((payload.sources.textSegment default []) joinBy "\n") ++ "\n If no content is provided, respond kindly that you don't have enough knowledge about MuleSoft "```   |

    Your flow should now look like the following:

    ![]({{ page.assets}}/7.png)

## Test the agent

1.  Run the project and check it starts without any errors. 
    If prompted select "Start new" in case your Mule runtime was already running.

    ![]({{ page.assets}}/8.png)

    {: .note }
    You might get an error like `Invalid input "++ ‘", expected FieldName, Function Call`. This is most likely due to copying from this document which changes the unicode character for quote and double quotes.. If that happens ensure to delete and retype any quote or double quotes you copied directly in the XML (ask the instructor for guidance):

1.  We are now ready to populate our Vector DB store but first download a fictitious product information document for a product called Mulesoft TXY, as this is the document we will use to test RAG

    Download MulesoftTXY.pdf from: <https://bit.ly/40wlkTO> 
    
    **Have a quick look at this document and see what details it contains**

    In order to use this file we need to upload this PDF into the location where Anypoint Code Builder is running. In order to do this, right click on the **resources** folder in Explorer and select **Upload**.

    ![]({{ page.assets}}/9.png)

    Select the file you just downloaded ensuring the name of the file is **MulesoftTXY.pdf**. Once uploaded the file should be visible in your project tree:

    ![]({{ page.assets}}/10.png)

1.  Restart the application:
2.  Open the **tests.http** file and run the `/api/rag/store/init` test

    ![]({{ page.assets}}/11.png)

    As you can see from the screenshot above, if everything goes well you should get a 200 response

1.  Lets see what our agent knows about MuleSoft TXY

    Run the next test `/api/rag/chat` and you should get either a negative answer (i.e. LLM doesn’t know anything about MuleSoft XXY) or a generic answer that doesn’t have anything to do with MuleSoft TXY (i.e. hallucination):

    ![]({{ page.assets}}/12.png)

1.  Now we’ll populate our embedding store and retry asking the LLM some questions.

    Invoke the `/api/rag/store/add-chunks` API

    ![]({{ page.assets}}/13.png)

1.  Now we can ask our LLM some more intelligent questions

    ![]({{ page.assets}}/14.png)

    Send this and you should see something like:

    ![]({{ page.assets}}/15.png)

    

Amazing job! You’ve built your first agent using the RAG approach for grounded responses!

**Congratulations**! you have finished both labs!!
