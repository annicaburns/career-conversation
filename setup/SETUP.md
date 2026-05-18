# Setup instructions for Mac

_If you're looking at this in Cursor, please right click on the filename in the Explorer on the left, and select "Open preview", to view the formatted version._

If you're new to developing on your Mac, you may need to install XCode developer tools. Here are [instructions](https://chatgpt.com/share/67b0b8d7-8eec-8012-9a37-6973b9db11f5).

One "gotcha" to keep in mind: if you run anti-virus software, VPN or a Firewall, it might interfere with installations or network access. Please temporarily disable if you have problems.



### Install Cursor

1. Visit cursor at https://www.cursor.com/
2. Click Sign In on the top right, then Sign Up, to create your account
3. Download and follow its instructions to install and open Cursor
4. Open the folder where this project exists
5. When your project opens, you may be prompted to "install recommended extensions" for Python and Jupyter. If so, choose Yes! Otherwise:
6. Open extensions (View >> extensions)
7. Search for python, and when the results show, click on the ms-python one, and Install it if not already installed
8. Search for jupyter, and when the results show, click on the Microsoft one, and Install it if not already installed


### Install `uv`

https://docs.astral.sh/uv/getting-started/installation/


### Project Setup

1. Within Cursor, select View >> Terminal, to see a Terminal window within Cursor.  
2. Type `pwd` to see the current directory, and check you are in the directory where the project lives
3. Start by running `uv self update` to make sure you're on the latest version of uv.
4. Run `uv sync`. If necessary, uv should install python 3.12, and then it should install all the packages.  

Just FYI on using uv:  
With uv, you do a few things differently:  
- Instead of `pip install xxx` you do `uv add xxx` - it gets included in your `pyproject.toml` file and will be automatically installed next time you need it  
- Instead of `python my_script.py` you do `uv run my_script.py` which updates and activates the environment and calls your script  
- You don't actually need to run `uv sync` because uv does this for you whenever you call `uv run`  
- It's better not to edit pyproject.toml yourself, and definitely don't edit uv.lock. If you want to upgrade all your packages, run `uv lock --upgrade`
- uv has really terrific docs [here](https://docs.astral.sh/uv/) - well worth a read!


### Create a local `.env` file

When you have the key, it's time to create your `.env` file:

1. In Cursor, go to the File menu and select "New Text File".

Type the following, being SUPER careful that you get this exactly right:

`OPENAI_API_KEY=`

And then after the equals sign, paste in your key from OpenAI. So after you've completed this, it should look like this:

`OPENAI_API_KEY=sk-proj-lots_of_characters_here`

But obviously the stuff to the right of the equals sign needs to match your key exactly.

If you have other keys, you can add them too:  
```
GOOGLE_API_KEY=xxxx
ANTHROPIC_API_KEY=xxxx
DEEPSEEK_API_KEY=xxxx
```

2. Now go to File menu >> Save As.. and save the file in the project root directory) with the name `.env`  

**IMPORTANT: be sure to Save the .env file after you edit it.**

