# user-record-app
Frontend Coding Assessment

# Requirements
Vue CLI and Node JS

# Instructions
In the root directory of the folder, run "npm install"
- This installs bootstrap

Then cd frontend-assessment, run "npm install"
- This installs nodemodules required

Then run "npm init @eslint/config"

![image](https://github.com/Dextre534/user-record-app/assets/91522845/448dba1b-6cc5-43ec-8317-8282fcacfdd6)

These are the options I selected. 
An .eslintrc.json file should be created

In the file, change the parser options to this
"parserOptions": {
        "ecmaVersion": 6,
        "sourceType": "module",
        "ecmaFeatures": {
            "modules": true
        }
    }


Then run "npm run serve" and access the app through links provided in terminal

# Past problems

The error that pops up has something to do with ESLint

I have tried to run 

- npm install eslint -g -D
- eslint --init

but so far it's not working..
