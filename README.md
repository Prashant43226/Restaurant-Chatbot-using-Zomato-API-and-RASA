# Restaurant-Chatbot using Zomato API and RASA

This is the **Complete Version** of the Chatbot.

Complete Flow is described by:
<p align="center">
  <img width="600" height="600" src="restaurant chatbot.png" alt="Conversation diagram">
</p>

## Setup and installation

If you are a Windows user,Then install Anaconda navigator .

For creating the bot, we need to install Python, RASA NLU and spaCy language models along with few dependencies. It would be good to create a separate virtual environment so as to keep the installations clean and together at one place. I will be using Conda to do the setup and installations. You are free to use virtualenv for the same as well.

# Create Virtual environment with python 3.6
```
conda create –name chatbot_env python=3.6
```
# Activate the environment
```
conda activate chatbot_env
```

Then from your Virtual Environment open a terminal in your folder 

If you haven’t installed Rasa NLU and Rasa Core yet, you can do it by navigating to the project directory and running:  
```
pip install -r requirements.txt
```

You also need to install a spaCy English language model. You can install it by running:

```
python -m spacy download en
```
You might find dependency issues.

The following dependency issues might arise:

If you are using Python>=3.8 consider degrading it as Tensorflow 2.0.0 does not support this.From terminal 
```
conda install python=3.5.0
```
Another dependency issue might arise after installing Spacy and creating a link.In this case :

1.Go to your Anaconda command prompt for your chatbot environment(in this case :Anaconda command prompt(chatbot_env))
2.Open the prompt in Administrator mode.
3.Create a symbolic link between your Python\Python36\site_packages\spacy\data and envs\rasa\Lib\site-packages\en_core_web_md using the makelink command as given below
```
mklink /d C:\Users\username\AppData\Roaming\Python\Python36\site-packages\spacy\data\en C:\Users\username\Anaconda3\envs\rasa\Lib\site-packages\en_core_web_md
```
### Files for Rasa NLU model

- **data/nlu_data.md** file contents training data for the NLU model.
	
- **nlu_config.yml** file contains the configuration of the Rasa NLU pipeline:  
```yaml
language: "en"

pipeline: spacy_sklearn
```	

### Files for Rasa Core model

- **data/stories.md** file contains some training stories which represent the conversations between a user and the assistant. 
- **domain.yml** file describes the domain of the assistant which includes intents, entities, slots, templates and actions the assistant should be aware of.  
- **actions.py** file contains the code of a custom action which retrieves results of the latest IPL match by making an external API call.
- **endpoints.yml** file contains the webhook configuration for custom action.  
- **policies.yml** file contains the configuration of the training policies for Rasa Core model.

## How to run locally

**Note**: If running on Windows, you will either have to [install make](http://gnuwin32.sourceforge.net/packages/make.htm) or copy the following commands from the [Makefile](https://github.com/Prashant43226/Restaurant-Chatbot-using-Zomato-API-and-RASA/blob/main/Makefile)

1. You can train the Rasa NLU model by running:  
```make train-nlu```  
This will train the Rasa NLU model and store it inside the `/models/current/nlu` folder of your project directory.

2. Train the Rasa Core model by running:  
```make train-core```  
This will train the Rasa Core model and store it inside the `/models/current/dialogue` folder of your project directory.

3. In a new terminal start the server for the custom action by running:  
```make action-server```  
This will start the server for emulating the custom action.

4. Test the assistant by running:  
```make cmdline```  
This will load the assistant in your terminal for you to chat.

You can also run the following from terminal

1.You can train the Rasa model using
train rasa

2.train rasa nlu

3.train rasa core

```
This chatbot project is still under development.
