---
layout: post
title:  "Exercise 1"
categories: workshop
assets: "./images/exercise1"
---
# MuleSoft AI Chain hands-on lab - Exercise 1

In this exercise you will use [Anypoint Code Builder](https://docs.mulesoft.com/anypoint-code-builder/) along with the [Mule AI Chain](https://mac-project.ai/) project to create some simple LLM integrations using MuleSoft

1.  Login to <https://eu1.anypoint.mulesoft.com> using the credentials given by the workshop leader. Accept cookies if prompted. If prompted to verify email address, click “Not Now”

2.  Click Get Started for Code Builder from the Anypoint landing page. Then click Launch - this will launch the cloud version of ACB which we will be using today

    ![]({{ page.assets }}/1.png)

    If prompted to “trust authors of the files in this folder” click “Yes, I trust the authors”

4.  (Optional) Choose a theme

5.  Click on the Mule logo in the Left-hand toolbar <img src="{{ page.assets}}/mule-logo.png"> and you will see the option appear to “Implement an API”. Click on “Implement an API”

    ![]({{ page.assets }}/2.png)

6.  If you get prompted with the following message, click on Allow:

    ![]({{ page.assets }}/3.png)

    then Open:

    ![]({{ page.assets }}/4.png)

7.  Set the Project name to **\<YOUR INITIALS\>-MuleAI Agent API Impl** and ensure the project location is set to **/home/\<login username\>** (the user you logged in as)

8.  In the Search an API box click in the Search Asset by name and type Mule AI Agent

9.  Select the API whose organization matches the name of the Anypoint Organization set up for this workshop (i.e. not Mulesoft). In the following screenshot that would be the first occurrence:

    ![]({{ page.assets }}/5.png)

10. Hover over the asset and select Add Asset as shown in the picture above.

11. Leave other values as defaults and click “Create Project”

    ![]({{ page.assets }}/6.png)

    If prompted to “trust authors of the files in this folder” tick the “Trust the authors of all files in the parent folder” checkbox and then click on “Yes, I trust the authors” 

    ![]({{ page.assets }}/7.png)

    and/or 

    This dialog box appears, select “Allow”, “Open” and then close the page as prompted.

    ![]({{ page.assets }}/8.png)

12. Wait until indexing has completed. You should now see the screen below:

    ![]({{ page.assets }}/9.png)

    MuleSoft has scaffolded an API structure for you which will take care of performing message validation and routing. This allows you to focus on the business logic rather than spending time with tedious checks and controls.

13. Now click on the Flow List icon that appears on the top right of the flow pane and select the **“post:\\chat”** flow as shown below:

    ![]({{ page.assets }}/10.png)

    {: .note}
    It’s very important that you don’t select **post:\\rag\\chat**. We will implement this API in the next exercise

14. Remove the existing Transform Message component by right clicking on it and selecting Delete Component

    ![]({{ page.assets }}/11.png)

15. Click the “**+**” to create the first step in the process. Select the icon <img src="images/exchange.png"> to access Exchange and search for MuleSoft AI Chain 

    ![]({{ page.assets }}/12.png)

    Open the MuleSoft AI Chain connector and add the “Tools use ai service”.

    {: .note}
    Ensure you **DON’T** select the “Tools use ai service (Legacy)” operation

16. Now click on the new connector added to the pane and click on the “+” button next to “Add Connector Config”:

    ![]({{ page.assets }}/13.png)

    Enter the following values:

    |                     |                                                                                                                                                            |
    | :-----------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------: |
    |   **Name**          |   MuleChain-Azure-AI-Config                                                                                                                                |
    |   **LLM Type**      |   AZURE\\_OPENAI                                                                                                                                            |
    |   **Config type**   |   Configuration json                                                                                                                                       |
    |   **File path**     |   ```mule.home ++ '/apps/' ++ app.name ++ '/muleChain.json'     Ensure you click on the small “*fx*” button to enable the expression language on this field ```  |
    |   **Model name**    |   gpt-4o                                                                                                                                                   |

    Your configuration screen should look like this:

    ![]({{ page.assets }}/14.png)

17. Click on Add

18. Set the data field to **payload.prompt**

19. Click on the “***fx***” button next to Tool config and paste this value:

    ```mule.home ++ '/apps/' ++ app.name ++ '/tools.json'```

    The connector configuration should look like this:

    ![]({{ page.assets }}/15.png)    

    Now we need to create the two configuration files needed by Mule AI Chain: **tools.json** and **muleChain.json**
    We will also need to use a test file to invoke our agent!

    Download the **muleChain.json** file [here](https://gist.githubusercontent.com/nbalestra/9e74b7c25afde0ca3e478b84b5e04a56/raw/3e4f4da7074b0eec0560d5b12e6a784fd83e7b60/muleChain.json) and the **tools.json** file from [here](https://gist.githubusercontent.com/nbalestra/86671d331b838af2d3616c8690e79960/raw/2e9dc51ad8d6e8fe35f7a547ad330a2c76810cc2/tools.json) (press CMD+S on Mac or CTRL+S on Windows)

    Download the **tests.http** file from [here](https://gist.githubusercontent.com/nbalestra/66e772536b9387b17c5c9e5675755d62/raw/e9f1d33acb33135ea9dc432ccf51f537d592d05c/tests.http) and save the page (eg: CMD+S if you are on Mac/CTRL+S if you’re on Windows). Ensure the file name is **tests.http** (remove any extension the browser is automatically appending to the file name)

20. Now right click on the **resources** folder in Explorer and select **Upload**

    ![]({{ page.assets }}/16.png)

21. Select **tools.json**, **muleChain.json** and **tests.http** from your file system and click on Open.

    We are finally ready to test our agent\!

24. In the file explorer, select the **tests.http** file that you downloaded earlier.

25. Click on the Debug icon you will find at the right of the screen

    ![]({{ page.assets }}/17.png)

26. And then on the Run button

    ![]({{ page.assets }}/18.png)

27. In the **OUTPUT** window at the bottom of the screen you should see that the project has built successfully: 

    ![]({{ page.assets }}/19.png)

    And in the TERMINAL window you should see that the project is **DEPLOYED**. This is now running in the cloud

    ![]({{ page.assets }}/20.png)

28. Once the application has been successfully deployed open the **tests.http** and click on the play button next to each test for Exercise 1 to execute a set of queries to your new agent which is now capable of answering questions about a fictitious customer’s orders!

    ![]({{ page.assets }}/21.png)

Ensure you only execute the tests referencing Exercise 1 since we still haven’t implemented Exercise 2

**Well done!** 

You have built your first autonomous agent in MuleSoft!

You can now move to the next exercise

