# Emobot French Emotional Audio Dataset Labeling

## Objective

**Label each audio sample with its corresponding emotion**, both categorically and on the Valence-Arousal scale.

### What is Valence-Arousal ?

**Arousal** (or intensity) is the level of “activation” of the emotion, and **ranges from calm/low (rated -3) to excited/high (rated +3)**.

**Valence** is the level of pleasantness of the emotion and **ranges from negative (rated -3) to positive (rated +3)**.
<br>

There are also *2 optional labels* related to quality, in case the sample is not clean or noisy.

## 0 - Create your working folder

Create a **new folder** on your computer that will be used for the rest of this process (to install Label Studio, download the dataset, store the labeling, etc).
Keep the **absolute path** to this folder at hand as it will be useful later on (you can copy/paste it from your explorer).

## 1 - Install Label Studio

The **complete installation guide** can be found [here](https://labelstud.io/guide/install#Install-with-pip).

### Launch a terminal and navigate to your working folder
```bash
cd "<ABSOLUTE_PATH_TO_YOUR_WORKING_FOLDER>"
```
where  `<ABSOLUTE_PATH_TO_YOUR_WORKING_FOLDER>` is the absolute path to the working folder you created in step 0 (make sure to *leave the quotation marks* around the path).

### Simple installation

`pip install label-studio`

### Virtualenv installation (recommended)

- **Windows**

	```bash
	python -m venv env
	source env/Scripts/activate
	python -m pip install label-studio
	```
	**NOTE : If your are using the default Command Prompt** instead of a bash Command Prompt, you need to replace `source` with `call` in the above command, like this : `call env/Scripts/activate`

- **Linux/MacOS**
	```bash
	python -m venv env
	source env/bin/activate
	python -m pip install label-studio
	```


## 2 - Run Label Studio

 1. Open a terminal

2. If you installed Label Studio in a **virtualenv**, you need to activate it :
	- Windows : 
		- Default Command Prompt : `call env/Scripts/activate`
		- Bash Command Prompt : `source env/Scripts/activate`
		
	- Linux/MacOS : `source env/bin/activate`

3. **Execute** these two commands :

```bash
export LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED=true
export LABEL_STUDIO_LOCAL_FILES_DOCUMENT_ROOT="<ABSOLUTE_PATH_TO_YOUR_WORKING_FOLDER>"
```
You need to **replace** `<ABSOLUTE_PATH_TO_YOUR_WORKING_FOLDER>` in the above command with the absolute path to the working folder you created in step 0.
Make sure to **leave the quotation marks** around the path (it helps dealing with potential spaces in your path).

**NOTE : when using Windows and the default Command Prompt**, you must replace `export` with `set` like this :
```bash
set LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED=true
set LABEL_STUDIO_LOCAL_FILES_DOCUMENT_ROOT="<ABSOLUTE_PATH_TO_YOUR_WORKING_FOLDER>"
```
 
4. **Run** the command : `label-studio`

5. A **window should open** in your default browser displaying Label Studio's interface


## 3 - Create an account and/or login

When you first start Label Studio, you will see the **sign up** screen.

1.  **Create an account** with your email address and a password.
2.  Log in to Label Studio.

Next time you launch Label Studio, you can directly login. The account is stored locally on your computer.


## 4 - Create a new project

1. In the top right corner, click  **Create**.
2. Type a project name.
3. Click  **Save**  to save your project.


## 5 - Setup the interface

1. In the top right corner, click **Settings**.
2. From the left side menu, choose **Labeling Interface**.
3.  Make sure the **Code** view is selected (and not *Visual*).
4. Replace the content of the text box with the following :

```xml
<View>
  <Audio name="audio" value="$audio"/>
	
  <Choices name="sentiment" toName="audio" choice="single" showInLine="true">
    <Choice value="Anger" style="zoom: 1.5;" hotkey="1"/>
    <Choice value="Happiness" style="zoom: 1.5;" hotkey="2"/>
    <Choice value="Sadness" style="zoom: 1.5;" hotkey="3"/>
    <Choice value="Neutral" style="zoom: 1.5;" hotkey="4"/>
    <Choice value="Fear" style="zoom: 1.5;" hotkey="5"/>
  </Choices>

  <Text name="Valence" value="Valence"/>
  <Choices name="valence" toName="audio" choice="single" showInLine="true">
    <Choice value="-3" style="zoom: 1.5;" hotkey="a"/>
    <Choice value="-2" style="zoom: 1.5;" hotkey="z"/>
    <Choice value="-1" style="zoom: 1.5;" hotkey="e"/>
    <Choice value="0" style="zoom: 1.5;" hotkey="r"/>
    <Choice value="1" style="zoom: 1.5;" hotkey="t"/>
    <Choice value="2" style="zoom: 1.5;" hotkey="y"/>
    <Choice value="3" style="zoom: 1.5;" hotkey="u"/>
  </Choices>
  
  <Text name="Arousal" value="Arousal"/>
  <Choices name="arousal" toName="audio" choice="single" showInLine="true">
    <Choice value="-3" style="zoom: 1.5;" hotkey="q"/>
    <Choice value="-2" style="zoom: 1.5;" hotkey="s"/>
    <Choice value="-1" style="zoom: 1.5;" hotkey="d"/>
    <Choice value="0" style="zoom: 1.5;" hotkey="f"/>
    <Choice value="1" style="zoom: 1.5;" hotkey="g"/>
    <Choice value="2" style="zoom: 1.5;" hotkey="h"/>
    <Choice value="3" style="zoom: 1.5;" hotkey="j"/>
  </Choices>

  <Text name="Quality" value="Quality"/>
  <Choices name="quality" toName="audio" choice="multiple" showInLine="true">
    <Choice value="not clean" style="zoom: 1.5;" hotkey="w"/>
    <Choice value="contains noise" style="zoom: 1.5;" hotkey="x"/>
  </Choices>
  
</View>
```
#### Your interface preview should look like this :
![Labeling interface](https://eapi.pcloud.com/getpubthumb?code=XZuwv1Zwp0BQygfVmX2VSAJGFVjrjfpJxd7&linkpassword=undefined&size=604x292&crop=0&type=auto)

5. Hit **Save** under the text box.
6. You can now go back to your project page by **clicking on your project's name** in the top bar (`Projects / Project name`).


## 6 - Download and import the dataset

1. **Download** the dataset from this link : https://e.pcloud.link/publink/show?code=XZQev1ZOHlKqkQ6ihhu9ztiLBjOOyMdVjpy

2. **Extract** it on your computer, inside of the working folder you created in step 0.
**The extracted folder containing all the audio samples must be a sub-folder of your working folder** created in step 0.

3. In Label Studio, at the project home page, in the top right corner, click **Settings**.

4. From the left side menu, choose **Cloud Storage**.

5. Click on the **Add Source Storage**.

6.  In the dialog box that appears, select  **Local Files**  as the storage type.

7.  In the **Absolute local path** field, paste the *absolute path* to the folder containing all the audio samples.

8.  Toggle the **Treat every bucket object as a source file** option to enable it.

9.  Click  **Add Storage**. This should close the dialog box.

10. In the grey box that appeared, click the **Sync Storage** button to launch the import of the dataset into Label Studio.

11. **Wait** for the sync process to complete. It should take **~2min**. Once it's completed, the **Status** should indicate `Completed` and the **Sync Storage** button should return to normal.

12. Return to the **project home page** by clicking on the project name in the top bar (`Projects / Project name`).

## 7 - Start labeling

In Label Studio, on the home page, click on **Label All Tasks** near the top, and start labeling the samples.


## 8 - Export your labels

- Once you finished labeling all the samples, return to the home page and click on the **Export** button near the top on the right.

- Select `CSV` format and hit the **Export** button in the bottom right.

- **Save the .csv file** to the desired location on your computer and send it by email
