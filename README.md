# streamlitbot

## Introduction
Streamlitbot est un projet de chatbot interactif développé en Python et Streamlit. L'objectif est de construire un chatbot basé sur GPT tout en explorant les fonctionnalités de Streamlit pour des interfaces simples et efficaces.

### Membres de l'équipe
- Adem HAJ BOUBAKER
- Nacir JAZA
- Mohamed Dhia ZELLAMA

## Pré-requis
Avant de commencer, assurez-vous d'avoir les éléments suivants installés sur votre machine :

- Python (version 3.7 ou plus)
- Pip (gestionnaire de paquets Python)
- Git

## Installation

### 1. Cloner le dépôt GitHub

```bash
cd Documents/git
mkdir projet_chatbot
cd projet_chatbot
git init
git clone https://github.com/AdemHB92/test.git
```
### 2. Réalisez le workflow

```bash
git status
git add .
git commit -m "initial commit"
git status
git remote -v
git remote add origin https://github.com/AdemHB92/test.git
git push origin master ( Monsieur pour votre cas c'est main je pense!)

```
### 3. Créer un environnement virtuel

```bash
cd streamlitbot
python -m venv stenv
source stenv/Scripts/activate
```

### 4. Ajouter un fichier `.gitignore`

Créez un fichier `.gitignore` pour exclure certains fichiers du dépôt Git.

```bash
touch .gitignore
nano .gitignore
```
Ajoutez les lignes suivantes :

```
# Python venv
stenv

# Streamlit secrets
.streamlit
```
![image](https://github.com/user-attachments/assets/0daa12bc-ddaa-4dd0-b56e-67b9bac51bab)


Sauvegardez et fermez (CTRL + O, puis CTRL + X).

### 5. Installer les dépendances
Créez un fichier `requirements.txt` et ajoutez les bibliothèques nécessaires comme `streamlit`.

```bash
touch requirements.txt
nano requirements.txt
```
Ajoutez :

```
streamlit
```

Ensuite, installez les dépendances :

```bash
pip install -r requirements.txt
```

## Lancement de l'application
Pour vérifier que Streamlit est bien installé :

```bash
streamlit hello
```

## Gestion des branches
Pour chaque fonctionnalité, une nouvelle branche est créée. Voici un exemple de workflow :

### Version 1 : Chatbot basique

1. Créer la branch version1

```bash
git branch version1
git checkout version1
```
2. Créer le fichier :

```bash
touch chatbot.py
nano chatbot.py
```

3. Ajouter le code correspondant.
```
import streamlit as st

st.title("Echo Bot")

# Initialize chat history
if "messages" not in st.session_state:
    st.session_state.messages = []

# Display chat messages from history on app rerun
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])
```
4. Ajouter les changements :

```bash
git add .
git commit -m "premiere version de mon chatbot"
git status
```

5. Pousser les modifications :

```bash
git push origin version1
```

6. Fusionner avec la branche principale :

```bash
git checkout main
git merge version1
```

### Version 2 : Ajout de l'interaction utilisateur

1. Créer une nouvelle branche :

```bash
git branch version2
git checkout version2
```

2.  modifier le fichier :

```bash
nano chatbot.py
```

3. Ajouter le code correspondant.
```
# React to user input
if prompt := st.chat_input("What is up?"):
    # Display user message in chat message container
    with st.chat_message("user"):
        st.markdown(prompt)
    # Add user message to chat history
    st.session_state.messages.append({"role": "user", "content": prompt})
```
4. Ajouter les changements :

```bash
git add .
git commit -m "deuxieme version de mon chatbot"
git status
```

5. Pousser les modifications :

```bash
git push origin version2
```

6. Fusionner avec la branche principale :

```bash
git checkout main
git merge version2
```

### Version 3 : Réponse dynamique

1. Créer une nouvelle branche :

```bash
git branch version3
git checkout version3
```

2.  modifier le fichier :

```bash
nano chatbot.py
```

3. Ajouter le code correspondant.
```
response = f"{prompt}"
# Display assistant response in chat message container
with st.chat_message("assistant"):
    st.markdown(response)
# Add assistant response to chat history
st.session_state.messages.append({"role": "assistant", "content": response})
```
4. Ajouter les changements :

```bash
git add .
git commit -m "troisieme version de mon chatbot"
git status
```

5. Pousser les modifications :

```bash
git push origin version3
```

6. Fusionner avec la branche principale :

```bash
git checkout main
git merge version3
```

### Version 4 : Intégration de l'API OpenAI
1. crée le fichier chatbotgpt.py

```bash
    touch chatbotgpt.py
```

2. modifié le fichier requirements.txt
```bash
nano requirements.txt
pip install -r requirements.txt
```

3. Ajouter un fichier `secrets.toml` dans un dossier `.streamlit` :

```bash
mkdir .streamlit
cd .streamlit
touch secrets.toml
nano secrets.toml
```
4. modifié le fihcier .gitignore
```bash
  cd ..
  nano .gitgnore
```
Ajoutez votre clé API OpenAI :

```
OPENAI_API_KEY = "YOUR_API_KEY"
```

5. Créer une nouvelle branche :

```bash
git branch version4
git checkout version4
```

6.  modifier le fichier :

```bash
nano chatbotgpt.py
```

7. Ajouter le code correspondant.
```
import streamlit as st
from openai import OpenAI

st.title("ChatGPT-like clone")

# Set OpenAI API key from Streamlit secrets
client = OpenAI(api_key=st.secrets["OPENAI_API_KEY"])

# Set a default model
if "openai_model" not in st.session_state:
    st.session_state["openai_model"] = "gpt-3.5-turbo"

# Initialize chat history
if "messages" not in st.session_state:
    st.session_state.messages = []

# Display chat messages from history on app rerun
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])

# Accept user input
if prompt := st.chat_input("What is up?"):
    # Add user message to chat history
    st.session_state.messages.append({"role": "user", "content": prompt})
    # Display user message in chat message container
    with st.chat_message("user"):
        st.markdown(prompt)
```
8. Ajouter les changements :

```bash
git add .
git commit -m "premiere version de chatbotgpt"
git status
```

9. Pousser les modifications :

```bash
git push origin version4
```

10. Fusionner avec la branche principale :

```bash
git checkout main
git merge version4
```
11 .Executer le code:

```bash
streamlit run chatboxgpt.py
```
### Version 5 : Optimisation et options avancées

1. Créer une nouvelle branche :

```bash
git branch version5
git checkout version5
```

2.  modifier le fichier :

```bash
nano chatbotgpt.py
```
3. Ajouter le code correspondant.
```
 # Display assistant response in chat message container
    with st.chat_message("assistant"):
        stream = client.chat.completions.create(
            model=st.session_state["openai_model"],
            messages=[
                {"role": m["role"], "content": m["content"]}
                for m in st.session_state.messages
            ],
            stream=True,
            max_tokens = 200,
        )
        response = st.write_stream(stream)
    st.session_state.messages.append({"role": "assistant", "content": response})
```
4. Ajouter les changements :

```bash
git add .
git commit -m "Deuxieme  version de chatbotgpt"
git status
```

5. Pousser les modifications :

```bash
git push origin version5
```

6. Fusionner avec la branche principale :

```bash
git checkout main
git merge version5
```
7. Executer le code:

```bash
streamlit run chatboxgpt.py
```


- **Branches supplémentaires :**

```bash
# Selectbox
git branch selectbox
git checkout selectbox
nano chatbotgpt.py

git add .
git commit -m "Ajout du selectbox"
git status
git push origin selectbox

git checkout main
git merge selectbox
streamlit run chatbotgpt.py

# Slider
git branch slider
git checkout slider
nano chatbotgpt.py


git add .
git commit -m "Ajout du slider"
git status
git push origin slider

git checkout main
git merge slider
streamlit run chatbotgpt.py
```
