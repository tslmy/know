---
description: Suitable for UPenn users.
---

# Prepare Qualtrics Survey With Batch-Populated Questions

**Create a new Qualtrics Project.**

1. Log into [Qualtrics](https://upenn.qualtrics.com/) with your PennKey.
2. Click `Create Project` &gt; `Research Core` &gt; `Blank Survey Project`.
3. Give the project a name, say "10-K". Click `Create Project`.
4. Click on the newly created project. You will be taken to the "survey design" interface.
5. Edit the Default Question Block to show some welcome text.

![Give the project a name, say &quot;10-K&quot;. Click Create Project.](../../.gitbook/assets/image%20%2814%29.png)

![Edit the Default Question Block to show some welcome text.](../../.gitbook/assets/image%20%282%29.png)

**Import Questions.**

1. Use my Jupyter Notebook `Qualtrics.ipynb` to generate a `qualtrics_survey_question_list.txt`.
2. Click `Tools` &gt; `Import/Export` &gt; `Import Survey…`.
3. Select the `qualtrics_survey_question_list.txt` generated before. Click `Import`.

{% hint style="info" %}
It may take so long that the page throws a 504 \(TimeOut\) error waiting for the server to respond. Don't worry, as the uploaded TXT file is parsed on the server. 

If this happens to be the case, go back to [Control Panel](https://upenn.co1.qualtrics.com/ControlPanel/?Section=MyProjectsSection&ContextSection=MyProjectsSection). Refresh the page every so often, till you see your project reached the right number of Questions. When it has finished loading all the questions, click into the project.
{% endhint %}

**Randomize presentation of blocks.**

1. Click `Survey Flow`. Below `Show Block: Default Question Block`, click `Add Below` &gt; `Randomizer`.
2. Tick `Evenly Present Elements` on the randomizer.
3. Drag any date-named block to the randomizer. "Randomly present `0` of the following elements." should automatically increase from `0` to `1`.
4. Click `Save Flow`.

**Batch-edit stuff.**

1. `Tools` &gt; `Import/Export` &gt; `Export Survey`. You will see a `QSF` file downloaded.
2. Open it with a text editor. It's JSON, so you can just prettify it accordingly. \(Note that mixing spaces and tabs in indentation breaks the QSF file.\)
3. Locate

   ```javascript
   "Type": "Root",
   "FlowID": "FL_1",
   "Flow": [
   ```

4. Cut & paste all `{"Type": "Standard", …, "FlowID": "FL_..."}` blocks under the `"Flow": […]` of the `{"Type": "BlockRandomizer", …}` .

   ![](file:///Users/lmy/Desktop/Screen%20Shot%202019-04-15%20at%204.35.50%20PM.png?lastModify=1555361209)

5. ~~Edit the `{"Properties": {"Count": …}}` to `3`. This is because we have:~~
   * ~~one Default Block for welcome message,~~
   * ~~one Randomizer, and~~
   * ~~one Web Service call~~

     ~~in our root Flow.~~
6. Locate all `"QuestionType": "TE",` lines. Add the following snippet before the lines:

   ```javascript
     "Validation":
     {
         "Settings":
         {
        "ForceResponse": "ON",
        "ForceResponseType": "ON",
        "Type": "None"
         }
     },
   ```

7. Save.
8. Back to our survey design page. Click `Tools` &gt; `Import/Export` &gt; `Import Survey…`. Select the QSF file. Click `Import`. You will see new survey project uploaded and opened up.

![Locate \`&quot;FlowID&quot;: &quot;FL\_1&quot;,\`](../../.gitbook/assets/image%20%2811%29.png)

**Make sure we can trace our mturkers across Qualtrics and Mturk.**

1. In `Survey Flow`, create a new Element that calls a `Web Service` with the following details:
   * URL: `http://reporting.qualtrics.com/projects/randomNumGen.php`
   * Method: `GET`
   * Query Parameters \(You can tweak the values here\)
     * `min` = `1000000`
     * `min` = `9999999`
   * Set Embedded Data
     * `MTurkCode`=`random`
2. Remember to save the Flow.

![](file:///Users/lmy/Library/Application%20Support/typora-user-images/image-20190415161413303.png?lastModify=1555361209)

