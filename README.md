[![Penetration testing methodology](https://github.com/jinverar/Penetration-Testing-Scripts/blob/master/playable-snip.JPG)](https://youtu.be/G9JcTkrvYuc "PWK Scripts in a custom Juypter Notebook")

# Penetration-Testing-Scripts
My recon and vuln scripts

These files are ment to work with juypter notebook. The files within this project get imported into juypter or copy and paste into Juypter Markdown cells. Then duplicate the notebooks and when you select a target all you need to do is rename the title of the copy notebook to be //project//*ipaddress*//hostname//. Then use the ESC + F key and find and replace *target* with target-ipaddress.

Once the files are in Juypter then the first file to duplicate is called "1-external+recon+vuln-exploration.md" and after that it's just a simple copy and paste from 2,3,4 into the cells below the "1-External+Recon+vuln". Do this for whatever part of the kill chain you are working on. 

the current concept is to use juypter notebooks with markdown language and import pictures into cells above or below. This can aid in writing pentesting reports and keep us organized. 

The future concept is to leverage the power of Juypter which can import and read other files such as .html, .csv, or xml. Then the idea is to start importing scans and figure out how to parse them with juypter later on. We can create graphs and do big data analysis along with penetration testing.  

We can run juypter notebook from KALI or another local server and colaborate and share notebooks. 

[![Penetration testing methodology](https://github.com/jinverar/Penetration-Testing-Scripts/blob/master/playable2-snip.JPG)](https://youtu.be/YR2kNf9Wf5Q "Exploitation scripts in a custom Juypter Notebook")

# requirements

juypter notebook
```
pip3 install --upgrade pip

pip3 install jupyter
```

# run juypter

jupyter notebook

# enable ssl with juypter
```
openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mykey.key -out jupytercert.pem

jupyter notebook  --config=/home/*user*/.jupyter/jupyter_notebook_config.py --certfile=/home/*user*/.jupyter/jupytercert.pem --keyfile /home/*user*/.jupyter/mykey.key --ip=*ip*
```
# play with some juypter extentions
```
pip install jupyter_contrib_nbextensions

jupyter contrib nbextension install --user

pip install --upgrade six

jupyter nbextension list
```
# enable drag and drop with juypter
```
jupyter nbextension enable dragdrop
```
https://*ipaddress*:8888/nbextensions
```
make sure to uncheck the box unter configureable nbextensions > then enable drag and drop
```

Please help Contribute!

1. Fork it!
2. Create your feature branch: git checkout -b my-new-feature
3. Commit your changes: git commit -am 'Add some feature'
4. Push to the branch: git push origin my-new-feature
5. Submit a Pull Request
