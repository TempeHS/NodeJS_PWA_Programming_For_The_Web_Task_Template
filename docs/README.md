# INTRODUCTION TO node.JS AND PROGRESSIVE WEB APPS TUTORIAL

This guided tutorial will introduce HSC Software Engineering to the basics of developing websites with the [node.JS framework](https://nodejs.org/en). The tutorial has been specifically designed for requirements in the [NESA Software Engineering Syllabus](https://curriculum.nsw.edu.au/learning-areas/tas/software-engineering-11-12-2022/content/n12/fa6aab137e) and students in NSW Department of Education schools using eT4L computers.

A [list of popular PWA's](https://business.adobe.com/blog/basics/progressive-web-app-examples) (including Ube, Spotify, Facebook and Google Maps)

## Overview of Progressive Web Apps

A [Progressive Web Apps (PWAs)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps?ref=arctype.com) is an app that is built using web platform technologies, but that provides a user experience like that of a platform-specific app. Like a website, a PWA can run on multiple platforms and devices from a single codebase. Like a platform-specific app, it can be installed on the device, can operate while offline and in the background, and can integrate with the device and with other installed apps.

### Technical features of PWAs

Because PWAs are websites, they have the same basic features as any other website: at least one HTML page, which loads CSS and JavaScript. Javascript is the language of the web and is exclusively used for the client-side front end; python, in the web context, can only be used in the back end. Like a normal website, the JavaScript loaded by the page has a global Window object and can access all the Web APIs that are available through that object. The PWA standard as defined by [W3C Standards](https://www.w3.org/standards/) has some specific features additional to a website:

| Feature             | Purpose                                                                                                                                                                                                                                                                                                                                                       |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| manifest.json       | An app manifest file, which, at a minimum, provides information that the operating system needs to install the PWA, such as the app name, screen orientation and icon set for different-sized viewports.                                                                                                                                                      |
| serviceworker.js    | A service worker, which, at a minimum, manages the caching that enables an online and offline experience whilst also interfacing with API's such as the [notification web API](https://developer.mozilla.org/en-US/docs/Web/API/Notification). It's important to understand that this JS file cannot control the DOM of the application for security reasons. |
| Icons & screenshots | A set of icons and screenshots that are used when uploading to an app store and when installing it as a native application. It is these icons that will be used in the desktop or app launcher when installed.                                                                                                                                                |
| Installable         | Because of the information contained in the manifest.json all PWA's can be installed like a native app. They can also be packaged and uploaded to the Google, Microsoft & Apple app stores.                                                                                                                                                                   |
| Cached locally      | Because the service worker details all apps and pages to be cached (all pages must have a \*.html name), the app and its resources can be cached locally for quick load times. _Note backend apps where the web server serves all pages from the DNS root do not meet the PWA specification._                                                                 |

The below image illustrates how the servicework manages online and offline behaviour.

![A highlevel illustration of the service worker](/docs/README_resources/Progressive-Web-Apps-Architecture.png "The service worker handles the initial requests and sets the behaviour depending on if the app is on or offline.")

## Your end product

This screen capture shows how the final PWA will be rendered to the user.

![Screen capture of the finished PWA](/docs/README_resources/final_app.png "This is what your application will look like")

## Requirements

1. [VSCode](https://code.visualstudio.com/download)
2. [Python 3.x](https://www.python.org/downloads/)
3. [Node.js v.20.x +](https://nodejs.org/en/download/package-manager)
4. [GIT 2.x.x +](https://git-scm.com/downloads)

> [!Important]
> MacOS and Linux users may have a `pip3` soft link instead of `pip`, run the below commands to see what path your system is configured with and use that command through the project. If neither command returns a version, then likely [Python 3.x](https://www.python.org/downloads/) needs to be installed.
>
> ```bash
> pip show pip
> pip3 show pip
> ```

## Prior learning

1. Bash basics & using the GIT Bash shell in VSCode
2. SQL
3. HTML Basics
4. CSS Basics
5. Python

## STEPS TO BUILDING YOUR FIRST PWA

### Setup your environment

![Screen recording of setting up VSCode](/docs/README_resources/get_vscode_started.gif "Follow these steps to setup VSCode")

> [!Note]
> Helpful VSCode settings are configured in [.vscode/settings.json](/.vscode/settings.json), which will automatically apply if you are not using a custom profile. If you are using a custom profile, it is suggested you manually apply those settings to your profile, especially the \*.md file association, so the README.md default opens in preview mode and setting _bash_ as your default terminal.

1. Install the necessary extensions for this tutorial.

| Required Extensions                                                                                              | Suggested nodeJS Extensions                                                                            |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| [McCarter.start-git-bash](https://marketplace.visualstudio.com/items?itemName=McCarter.start-git-bash)           | [ecmel.vscode-html-css](https://marketplace.visualstudio.com/items?itemName=ecmel.vscode-html-css)     |
| [yy0931.vscode-sqlite3-editor](https://marketplace.visualstudio.com/items?itemName=yy0931.vscode-sqlite3-editor) | [ms-vscode.js-debug](https://marketplace.visualstudio.com/items?itemName=ms-vscode.js-debug)           |
| [medo64.render-crlf](https://marketplace.visualstudio.com/items?itemName=medo64.render-crlf)                     | [esbenp.prettier-vscode](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)\* |
|                                                                                                                  | [oderwat.indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow)   |

_\*You will need to configure esbenp.prettier-vscode as your default formatter_

2. Open a GIT BASH terminal

> [!Note]
> From now on, you should aim to run all commands from the CLI. You are discouraged from left/right clicking the GUI. You will find it feels slow at first, but through disciplined use, you will become much quicker and more accurate with CLI commands than GUI controls.

Make sure you open a new terminal with the keys <kbd>Ctrl</kbd> + <kbd>`</kbd> and choose Git Bash from the menu option in the top right of the terminal shell.

![Screen capture of the menu options for terminals](/docs/README_resources/git_bash_shell.png "Choose Git Bash from the list")

3. Get the working files, which include this README.md

   - Open a new window in VSCode
   - Choose your working directory

```bash
git clone https://github.com/TempeHS/NodeJS_PWA_Programming_For_The_Web_Task_Template.git
cd NodeJS_PWA_Programming_For_The_Web_Task_Template
```

> [!TIP]
> Alternatively, you can fork the [template repository](https://github.com/TempeHS/NodeJS_PWA_Programming_For_The_Web_Task_Template) to your own GitHub account and open it in a Codespace in which all dependencies and extensions will be automatically installed.

1. Inititalise a node application

```bash
npm init -y
```

5. Install necessary dependencies.

```bash
npm install sqlite3
npm install express
```

---

### Create files and folders for your node.JS Project

1. Make a folder for all your working documents like photoshop \*.psd files, developer documentation etc.

```bash
mkdir working_documents
```

2. Create a license file.

```bash
touch LICENSE
code LICENSE
```

Copy the [GNU GPL license](https://www.gnu.org/licenses/gpl-3.0.txt) text into the file. GNU GPL is a free software license, or copyleft license, that guarantees end users the freedom to run, study, share, and modify the software.

3. Create your directory structure and some base files using BASH scripts reading text files.

```text
├── database
├── working_documents
├── public
│   ├── css
│   ├── icons
│   ├── images
│   ├── js
│   ├── index.html
│   ├── about.html
│   ├── manifest.json
│   ├── serviceworker.js
├── LICENSE
└── index.js
```

4. Create a text file with a list of folders you need in the public folder of your project. The web server will serve the contents of the public folder. This folder is the 'FRONT END,' while all folders behind it are the 'BACK END.'

```bash
mkdir public
cd public
touch folders.txt
code folder.txt
```

4. Run a BASH script to read the text file and create the folders listed in it.

```bash
while read -r line; do
echo $line
mkdir -p $line
done < folders.txt
```

5. Populate the file with a list of files you need at the root of your project.

```bash
touch files.txt
code files.txt
```

6. Run a BASH script to read the text file and create the files listed in it.

```bash
while read -r line; do
echo $line
touch -p $line
done < files.txt\
```

> [!Important]
>
> —The last list item needs a line ending, so make sure the last line in the file is blank.
>
> - You will find that all file and folder names have an unwanted `space` character at the end. This is because you are using a BASH emulator on the Windows operating system. Bash is a Unix language that uses [LF Unicode character 000A while Windows uses CRLF Unicode characters 000D and 000A](https://learn.microsoft.com/en-us/visualstudio/ide/encodings-and-line-breaks?view=vs-2022). Because you have installed the [medo64.render-crlf](https://marketplace.visualstudio.com/items?itemName=medo64.render-crlf) extension, click on `CRLF` in the bottom bar of VSCode and choose `LF` to change the line ending before running your BASH script.

---

### Setup your SQLite3 Database

```bash
cd ..
mkdir database
cd database
touch data_source.db
```

> [!Note]
> The following SQL queries are provided as an example only. Students are encouraged to select their content and design a database schema for it; ideas include:
>
> - Favourite bands
> - Favourite movies
> - Favourite games
> - Favourite books
> - etc

1. To run SQLite3 SQL queries in VSCode
   Open the DB file, then choose "Query Editor" from the top menu.

```bash
code data_source.db
```

![Screen capture of query editor](/docs/README_resources/query_editor.png "Choose Query Editor from the top menu")

```sql
CREATE TABLE extension(extID INTEGER NOT NULL PRIMARY KEY,name TEXT NOT NULL, hyperlink TEXT NOT NULL,about TEXT NOT NULL,image TEXT NOT NULL,language TEXT NOT NULL);
```

2. After running each query put `--` infront of the query to turn it into a comment so it doesn't run again and error.
3. Run SQL queries to populate your table.

```sql
INSERT INTO extension(extID,name,hyperlink,about,image,language) VALUES (1,"Live Server","https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer","Launch a development local Server with live reload feature for static & dynamic pages","https://ritwickdey.gallerycdn.vsassets.io/extensions/ritwickdey/liveserver/5.7.9/1736542717282/Microsoft.VisualStudio.Services.Icons.Default","HTML CSS JS");
```

```sql
INSERT INTO extension(extID,name,hyperlink,about,image,language) VALUES (2,"Render CR LF","https://marketplace.visualstudio.com/items?itemName=medo64.render-crlf","Displays the line ending symbol and optionally extra whitespace when 'Render whitespace' is turned on.","https://medo64.gallerycdn.vsassets.io/extensions/medo64/render-crlf/1.7.1/1689315206970/Microsoft.VisualStudio.Services.Icons.Default","#BASH");
```

```sql
INSERT INTO extension(extID,name,hyperlink,about,image,language) VALUES (3,"Start GIT BASH","https://marketplace.visualstudio.com/items?itemName=McCarter.start-git-bash","Adds a bash command to VSCode that allows you to start git-bash in the current workspace's root folder.","https://mccarter.gallerycdn.vsassets.io/extensions/mccarter/start-git-bash/1.2.1/1499505567572/Microsoft.VisualStudio.Services.Icons.Default","#BASH");
```

```sql
INSERT INTO extension(extID,name,hyperlink,about,image,language) VALUES (4,"SQLite3 Editor","https://marketplace.visualstudio.com/items?itemName=yy0931.vscode-sqlite3-editor","Edit SQLite3 files like you would in spreadsheet applications.","https://yy0931.gallerycdn.vsassets.io/extensions/yy0931/vscode-sqlite3-editor/1.0.85/1690893830873/Microsoft.VisualStudio.Services.Icons.Default","SQL");
```

4. Run some SQL queries to test your database.

```sql
SELECT * FROM extension;
SELECT * FROM extension WHERE language LIKE '#BASH';
```

---

### Make your graphic assets

> [!Note]
> Graphic design is not the focus of this course. It is suggested that you do not spend excessive time designing logos and icons.

1. Use Photoshop or [Canva](https://www.canva.com/en_au/signup/?signupRedirect=%2Fedu-signup&loginRedirect=%2Fedu-signup&brandingVariant=edu) to design a simple square logo 1080px X 1080px named logo.png. Save all working files (\*.psd, pre-optimised originals, etc) into the working_documents directory.
2. Design a simplified app icon 512px X 512px named favicon.png.
3. Web optimise the images using [TinyPNG](https://tinypng.com/).
4. Save the files into the public/images folder.
5. Rename the 512x512 icon to icon-512x512.png, then resize and rename it as follows:
   - icon-128x128.png
   - icon-192x192.png
   - icon-384x384.png
   - icon-512x512.png
6. Web optimise the images using [TinyPNG](https://tinypng.com/).
7. Save the optimised icons to public/icons.
8. Save the optimised logo and favicon to public/images.

---

### Setup your core index.html

> [!Note]
> Adjust titles, headings and content to match your concept.

```bash
cd ../templates
touch layout.html
code layout.html
```

5. Insert the basic HTML structure in your index.html file.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <meta http-equiv="Content-Security-Policy" content="script-src 'self';" />
    <link rel="stylesheet" href="css/style.css" />
    <title>VSCode Extension Catalogue</title>
    <link rel="manifest" href="manifest.json" />
    <link rel="icon" type="image/x-icon" href="images/favicon.png" />
  </head>
  <body>
    <main>
      <!-- NAV START -->

      <!-- NAV END -->
      <div class="container"></div>
    </main>
    <script src="js/app.js"></script>
  </body>
</html>
```

---

### Style the HTML core

```bash
cd css
touch style.css
code style.css
```

1. Insert the css code into css/style.css.

```css
@import url("https://fonts.googleapis.com/css?family=Nunito:400,700&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background: #fdfdfd;
  font-family: "Nunito", sans-serif;
  font-size: 1rem;
}
main {
  max-width: 900px;
  margin: auto;
  padding: 0.5rem;
  text-align: center;
}
```

---

### Make and style the menu

```bash
cd ..
code index.html
```

1. Insert the menu HTML into index.html between the comment placeholders.

```html
<nav>
  <img src="images\logo.png" alt="VSCode Extensions site logo." />
  <h1>VSCode Extensions</h1>
  <ul class="topnav">
    <li><a href="#">Home</a></li>
    <li><a href="add.html">Add me</a></li>
    <li><a href="about.html">About</a></li>
  </ul>
</nav>
```

```bash
`cd ../../public/css`
`code style.css`
```

2. Style the menu by inserting this below your existing CSS in public/css/style.css.

```css
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
nav img {
  height: 100px;
}
nav ul {
  list-style: none;
  display: flex;
}
nav li {
  margin-right: 1rem;
}
nav ul li a {
  text-decoration-line: none;
  text-transform: uppercase;
  color: #393b45;
}
nav ul li a:hover {
  color: #14e6dd;
}
nav h1 {
  color: #106d69;
  margin-bottom: 0.5rem;
}
```

<HR

### Render your website

Express is a light weight webserver designed specifically for Node.js web applications. You have already installed it when you set up your environment.

```bash
cd ../..
code index.js
```

1. Insert the node.js to the backend index.js.

```js
// Insert additional backend js above the express server configuration

const express = require("express");
const path = require("path");
const app = express();
app.use(express.static(path.join(__dirname, "public")));

app.get("/", function (req, res) {
  res.sendFile(path.join(__dirname, "public/index.html"));
});
app.listen(5000, () =>
  console.log(
    "Server is running on Port 5000, visit http://localhost:5000/ or http://127.0.0.1:5000 to access your website"
  )
);
```

2. Run the built-in webserver.

```bash
node index.js
```

3. Visit your website and look at the source in developer tools to see how the page has been rendered.

---

### Query your SQL database and migrate the data for the frontend

> [!Note]
> From here students have two choices, they can use their existing Python skills or new JS skills. Either way, students will be querying a table in data_source.db and then constructing a JSON file that will be pushed to the frontend, ready for rending by a frontend JS script.
> If you choose the JS method, you should refer to the Python method in the future as a helpful way to have more complex Python programs in the backend and create a simple responsive GUI using HTML/CSS/JS.

#### Why JSON?

[JSON (JavaScript Object Notation)](https://www.json.org/json-en.html) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate. It is also very secure and the worflow used in this application ensures data integrity of the backend.

### Choose your backend implementation language:

<details>
    <summary><h3 style="display:inline">I want to use Python</h3></summary>

1. Install the Python SQLite3 requirements

```bash
pip install sqlite3
```

```bash
touch database_manager.py
code database_manager.py
```

2. Write the Python Script to query the SQL database and construct the JSON file.

```python
import sqlite3 as sql

con = sql.connect("database/data_source.db")
cur = con.cursor()
data = cur.execute('SELECT * FROM extension').fetchall()
con.close()
f = open("public/frontEndData.json", "w")
f.write("[\n")
for row in data:
    f.write('{\n')
    f.write(f'"extID":{row[0]},\n"name":"{row[1]}",\n"hyperlink":"{row[2]}",\n"about":"{row[3]}",\n"image":"{row[4]}",\n"language":"{row[5]}"\n')
    if row == data[len(data)-1]:
        f.write("}\n")
    else:
        f.write("},\n")
f.write("]\n")
f.close()
```

> [!Note]
> This approach is different from the Pythonic way to generate a JSON file. Because this approach is about algorithm design, it models how an algorithm can easily migrate data from one format/structure to another. If you know the Pythonic way, you can just implement it. However, software engineers should understand and be able to replicate data migration algorithms.

```bash
code index.js
```

2. Insert this Javascript above the express setup in index.js to execute the Python program.

> [!Important]
> This code must be above the Express server configuration and instantiation.

```js
const spawn = require("child_process").spawn;
// you can add arguments with spawn('python',["path/to/script.py", arg1, arg2, ...])
const pythonProcess = spawn("python", ["database_manager.py"]);
```

3. Test your application. The expected behaviour is a file called frontEndData.json filled with the table from data_source is saved in the /public folder. The JSON file should validate with [jsonlint](https://jsonlint.com/).

```bash
node index.js
```

</details>

<details>
  <summary><h3 style="display:inline">I want to use JavaScript</h3></summary>
  
```bash
code index.js
```

1. Insert this Javascript above the express setup in index.js to query the SQL database and construct the JSON file.

> [!Important]
> This code must be above the Express server configuration and instantiation.

```js
const sqlite3 = require("sqlite3").verbose();
const db = new sqlite3.Database("database/data_source.db");

let myString = "[\n";
db.all("SELECT * FROM extension", function (err, rows) {
  let myCounter = 0;
  rows.forEach(function (row) {
    // for debugging
    // console.log(row.extID + ": " + row.name + ": " + row.hyperlink + ": " + row.about + ": " + row.image + ": " + row.language);
    myString =
      myString +
      '{\n"extID":' +
      row.extID +
      ',\n"name":"' +
      row.name +
      '",\n"hyperlink":"' +
      row.hyperlink +
      '",\n"about":"' +
      row.about +
      '",\n"image":"' +
      row.image +
      '",\n"language":"' +
      row.language;
    myCounter++;
    if (myCounter == rows.length) {
      myString = myString + '"\n}\n';
    } else {
      myString = myString + '"\n},\n';
    }
  });

  // console.log(myString);
  var fs = require("fs");
  fs.writeFile("public/frontEndData.json", myString + "]", function (err) {
    if (err) {
      console.log(err);
    }
  });
});
```

2. Test your application. The expected behaviour is a file called frontEndData.json filled with the table from data_source is saved in the /public folder. The JSON file should validate with [jsonlint](https://jsonlint.com/).

```bash
node index.js
```

</details>

---

### Render the JSON data on the frontend

```bash
cd public/js
touch app.js
code app.js
```

1. Insert the js into public/js/app.js; this JS reads the JSON file and inserts it as HTML into the .container class `<DIV>`.

```js
let result = "";
fetch("./frontEndData.json")
  .then(function (response) {
    return response.json();
  })
  .then(function (data) {
    appendData(data);
  })
  .catch(function (err) {
    console.log("error: " + err);
  });
function appendData(data) {
  data.forEach(({ name, image, hyperlink, about, language } = rows) => {
    result += `
        <div class="card">
        <img class="card-image" src="${image}" alt="Product image for the ${name} VSCode extension."/>
        <h1 class="card-name">${name}</h1>
        <p class="card-about">${about}</p>
        <a class="card-link" href="${hyperlink}"><button class="btn">Read More</button></a>
        </div>
        `;
  });
  document.querySelector(".container").innerHTML = result;
}
```

```bash
cd ../css
code style.css
```

2. Style the cards by inserting this below your existing CSS in public/css/style.css.

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(15rem, 1fr));
  grid-gap: 1rem;
  justify-content: center;
  align-items: center;
  margin: auto;
  padding: 1rem 0;
}
.card {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 17rem;
  background: #fff;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
  border-radius: 10px;
  margin: auto;
  overflow: hidden;
}
.card-image {
  width: 100%;
  height: 15rem;
  object-fit: cover;
}
.card-name {
  color: #222;
  font-weight: 700;
  text-transform: capitalize;
  font-size: 1.1rem;
  margin-top: 0.5rem;
}
.card-about {
  text-overflow: ellipsis;
  width: 15rem;
  white-space: nowrap;
  overflow: hidden;
  margin-bottom: 1rem;
}
.btn {
  border: none;
  background: none;
  border-radius: 5px;
  box-shadow: 1px 1px 2px rgba(21, 21, 21, 0.1);
  cursor: pointer;
  font-size: 1.25rem;
  margin: 0 1rem;
  padding: 0.25rem 2rem;
  transition: all 0.25s ease-in-out;
  background: hsl(110, 21%, 93%);
  color: hsl(141, 100%, 22%);
  margin-bottom: 1rem;
}
.btn:focus,
.btn:hover {
  box-shadow: 1px 1px 2px rgba(21, 21, 21, 0.2);
  background: hsl(111, 21%, 86%);
}
.about-container {
  font-size: 1.25rem;
  margin-top: 2rem;
  text-align: justify;
  text-justify: inter-word;
}
```

---

### Finish the PWA code, so it is compliant with W3 web standards

1. Take a screenshot of the website. Then size the image to 1080px X 1920px, web optimise the images using [TinyPNG](https://tinypng.com/) and save it to public/icons.

```bash
cd ..
code manifest.json
```

2. Configure the manifest.json to the PWA standard by inserting the JSON below and validating the JSON with [jsonlint](https://jsonlint.com/). The manifest.json sets the configuration for the installation and caching of the PWA.

```json
{
  "name": "VSCode Extension Catalogue",
  "short_name": "vscodeextcat",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#fdfdfd",
  "theme_color": "#14E6DD",
  "orientation": "landscape-primary",
  "icons": [
    {
      "src": "icons/icon-128x128.png",
      "type": "image/png",
      "sizes": "128x128",
      "purpose": "maskable"
    },
    {
      "src": "icons/icon-128x128.png",
      "type": "image/png",
      "sizes": "128x128",
      "purpose": "any"
    },
    {
      "src": "icons/icon-192x192.png",
      "type": "image/png",
      "sizes": "192x192",
      "purpose": "maskable"
    },
    {
      "src": "icons/icon-192x192.png",
      "type": "image/png",
      "sizes": "192x192",
      "purpose": "any"
    },
    {
      "src": "icons/icon-384x384.png",
      "type": "image/png",
      "sizes": "384x384",
      "purpose": "maskable"
    },
    {
      "src": "icons/icon-384x384.png",
      "type": "image/png",
      "sizes": "384x384",
      "purpose": "any"
    },
    {
      "src": "icons/icon-512x512.png",
      "type": "image/png",
      "sizes": "512x512",
      "purpose": "maskable"
    },
    {
      "src": "icons/icon-512x512.png",
      "type": "image/png",
      "sizes": "512x512",
      "purpose": "any"
    }
  ],
  "screenshots": [
    {
      "src": "icons/desktop_screenshot.png",
      "sizes": "1920x1080",
      "type": "image/png",
      "label": ""
    },
    {
      "src": "icons/mobile_screenshot.png",
      "sizes": "1080x1920",
      "type": "image/png",
      "form_factor": "wide",
      "label": ""
    }
  ]
}
```

```bash
cd js
code app.js
```

2. Configure the app.js to initiate the servicework.js ny inserting the JS. This ensures that when the window (app) loads, the serviceworker.js is called to memory.

```js
if ("serviceworker" in navigator) {
  window.addEventListener("load", function () {
    navigator.serviceworker
      .register("js/serviceworker.js")
      .then((res) => console.log("service worker registered"))
      .catch((err) => console.log("service worker not registered", err));
  });
}
```

```bash
cd js
code serviceworker.js
```

1. Configure the serviceworker.js by inserting the JS. The serviceworker.js, as the name suggests, is the file that does all the work in a PWA, including caching and API integration for the [WEB APIs](https://developer.mozilla.org/en-US/docs/Web/API).

```js
const assets = [
  "/",
  "css/style.css",
  "js/app.js",
  "images/logo.png",
  "images/favicon.png",
  "icons/icon-128x128.png",
  "icons/icon-192x192.png",
  "icons/icon-384x384.png",
  "icons/icon-512x512.png",
  "icons/desktop_screenshot.png",
  "icons/mobile_screenshot.png",
];

const CATALOGUE_ASSETS = "catalogue-assets";

self.addEventListener("install", (installEvt) => {
  installEvt.waitUntil(
    caches
      .open(CATALOGUE_ASSETS)
      .then((cache) => {
        console.log(cache);
        cache.addAll(assets);
      })
      .then(self.skipWaiting())
      .catch((e) => {
        console.log(e);
      })
  );
});

self.addEventListener("activate", function (evt) {
  evt.waitUntil(
    caches
      .keys()
      .then((keyList) => {
        return Promise.all(
          keyList.map((key) => {
            if (key === CATALOGUE_ASSETS) {
              console.log("Removed old cache from", key);
              return caches.delete(key);
            }
          })
        );
      })
      .then(() => self.clients.claim())
  );
});

self.addEventListener("fetch", function (evt) {
  evt.respondWith(
    fetch(evt.request).catch(() => {
      return caches.open(CATALOGUE_ASSETS).then((cache) => {
        return cache.match(evt.request);
      });
    })
  );
});
```

---

### Validate your PWA

Validation is important to ensure the app is compliant to [W3 web standards](https://www.w3.org/standards/).

1. Open your website in Chrome, open developer tools (F12), and run a Lighthouse report.
   ![Screen capture of Chrome Lighthouse report](/docs/README_resources/Chrome_Lighthouse_Report.png "Click F12 and choose Lighthouse on the top menu of your developer tools").
2. Open your website in Edge, open developer tools (F12), and look at the application report.
   ![Screen capture of Chrome Lighthouse report](/docs/README_resources/Edge_Application_Report.png "Click F12 and choose Lighthouse on the top menu of your developer tools").

---

### Take your app further

The following code snippets will help you create a simple form on the add.html page. This form allows people to add their details to an email database for updates on your catalogue. Less explicit instructions have been provided; students are encouraged to practice their BASH, SQL, HTML, CSS, and JS to bring it all together. The screenshot below shows what the page should look like, and when users submit, the database is updated.

![Screen capture of the finished PWA](/docs/README_resources/form_example.png "This is what your application will look like").

1. Page specifications:
   - Simple form where the user inserts their name and email address
   - When they click submit the database is updated
   - The input form must be styled to be consistent with the rest of the website
   - A message confirming submission is returned to the user
2. SQL schema specifications:
   - A new table called contact_list
   - 3 columns
     - id is the primary key and should increment automatically
     - email must be unique
     - name

> [!Note]
> You will need to catch the expectation of a duplicate email

```bash
npm npm install body-parser
```

```js
let bodyParser = require("body-parser");
app.use(bodyParser.urlencoded({ extended: false }));
```

```js
res.sendFile(path.join(__dirname, "public/add.html"));
```

```js
app.post("/add.html", function (req, res) {
  db.serialize(() => {
    db.run(
      "INSERT INTO contact_list(email,name) VALUES(?,?)",
      [req.body.email, req.body.name],
      function (err) {
        if (err) {
          return console.log(err.message);
        }
        res.send(
          "Thank you " +
            req.body.name +
            " we have added your email " +
            req.body.email +
            " to our distribution list."
        );
      }
    );
  });
});
```

```html
<form action="/app.html" method="POST" class="box">
  <div>
    <label class="form-label">Email address</label>
    <input
      name="email"
      type="email"
      class="form-control"
      id="email"
      pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2, 4}$"
      placeholder="name@example.com"
    />
  </div>
  <div>
    <label class="form-label">Name</label>
    <textarea class="form-control" name="name" id="name" rows="1"></textarea>
  </div>
  <br />
  <div>
    <button type="submit" class="btn">Submit</button>
  </div>
</form>
```

```css
.form-control {
}
```

---

<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/TempeHS/Flask_PWA_Programming_For_The_Web_Task_Source">Node.js PWA Programming For The Web Task Source</a> and <a property="dct:title" rel="cc:attributionURL" href="https://github.com/TempeHS/Flask_PWA_Programming_For_The_Web_Task_Template">Node.js PWA Programming For The Web Task Template</a> by <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://github.com/benpaddlejones">Ben Jones</a> is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>
