# Getting started with `Docs as code`

Keep your technical documentation always in sync with UI changes. 

Pull the text of UI labels, hints, error messages, menu options, and so on from code and use them in your documentation as variables, so that when you build your techdoc pages, they are automatically updated with the code changes.

How?

<img src = "/images/docsAScode.png"/>

If your techdocs are written in Markdown or HTML, you can use the objects, tags, and filters of the Liquid template language in your doc files, and then build your techdocs with Jekyll (which understands Liquid). So, for example, if your techdoc has something like this:

`To access your tokens, go to {{ site.data.uitext.menu-account }} > {{ site.data.uitext.menu-security }}.`

it'll be rendered like this:

`To access your tokens, go to Account > Security.`

Tomorrow, if your UI changes, and `Account` is renamed to something like `Settings` or `Configuration`, all you'd need to do is to update the UI strings file that holds the mapping between the UI text IDs and the text (for example, a `.csv` or a `.json` file that contains the strings that you send across for translations). The moment you update this UI strings file, and run the Jekyll build, all your techdoc pages get updated automatically.

GitHub also uses the Jekyll rendering engine to handle the repo websites. This means, you can see this concept in use at https://aninditabasu.github.io/docs-as-code/.

To use the Jekyll rendering engine, your directory structure should follow a specific structure. The files in this repo are arranged in that structure, so if you want to experiment with migrating your techdocs to Liquid+Jekyll, feel free to use this repo as a template (or, fork it).

<hr/>

-  [Prerequisites](#prerequisites)
-  [How to use this repository as a template](#how-to-use-this-repository-as-a-template)
-  [How to customise the files for your documentation](#how-to-customise-the-files-for-your-documentation)
-  [Gotchas](#gotchas)
-  [Resources](#resources)

<hr/>

## Prerequisites

This template is meant for beginners. You need have a basic knowledge of Markdown, HTML, CSS, and JS; bonus if you are familiar with Bootstrap.

## How to use this repository as a template

This template contains the barest minimum files that you need for a variables-populated website up and running.

<pre>
- _data           # folder to contain data files
  -- en.json
- _layouts        # folder to contain HTML templates
  -- default.html
- css             # folder to contain stylesheets
  -- bootstrap.min.css
- images          # folder to contain images
  -- docsAScode.png
- topics          # folder to contain pages of the website
  -- page1.html
  -- page2.html
  -- page3.html
- js             # folder to contain Javascript files
  -- bootstrap.min.js
  -- jquery.min.js
  -- popper.min.js
- _config.yml    # basic configuration info
- index.html     # landing page of the website
</pre>

1. Scroll up, locate the **Use this template** button, and click it. If you don't see this button, scroll up further and sign in to GitHub (or, sign up).
2. Specify a repository name. The name you choose will be used in the URL of your website, like this: `https://<yourGithubID>.github.io/<yourRepositoryName>`.
3.  Click **Create repository from template**. The files and folders from this repository are copied over to a new repository for you.
In the new repository you just created, locate the **Settings** button and click it. Scroll down to the section called **GitHub pages** and, on the list for **Source**, ensure that **master branch** is selected.
4.  In the `_config.yml` file, put down your own name and replace the value of `baseurl` with the name of your repository. This name is the same as the one you specified in step 2 earlier.
5.  Navigate to `https://<yourGithubID>.github.io/<yourRepositoryName>`. What you see on the webpages is pretty much the same as what you saw at `https://aninditabasu.github.io/docs-as-code`. You now have a starting point to work with.

## How to customise the files for your documentation

1. Return to the **Code** page on the GitHub web interface, and edit the files so that they contain your own documentation:
   1.  Go to the `css` and `js` folders to look at the files there. This template uses the Bootstrap framework, and if you're familiar with the framework, it might be a good idea to retain the files in `css` and `js` till such time as you become more familiar with the files and folders. If you'd like to use any other stylesheets, replace the files with your own.
   2.  If you added your own files in the `css` or `js` folders, edit the `_layouts` > `default.html` file to add those file references in the `<head>` section.
   3. Edit the `_data` > `en.json` file as you deem fit. This file contains the variables that you'll use for your webpages. The entries in this file take the following format: `"variableID": "variable value"`, followed by a comma, except for the last entry, which does not have a comma at the end.
   4. Edit the files in the `topics` folder as you deem fit. Just use HTML or Markdown tags like you normally would, but retain the text of lines 1 through 4 as is. Do not touch them 🙂 Feel free to change anything from line 5 onwards. If you edited the `data` > `en.json` file, use those variables in these `.html` or `.md` files. 
   
      The format for calling the variables from the `en.json` file is like this: `{{ site.data.<filename>.<varID> }}`. For example, if your data file is called `menu_strings.json` and has an entry like `"hed_aria_label":"Admissions Coordinator"`, the format to use in your `.html` to populate the page with a text like `Admissions Coordinator` is like this: `{{ site.data.menu_strings.hed_aria_label }}`.
   5. In the root folder, edit the `index.html` file, which is used as the landing page of your website, as you deem fit. Again, do not touch lines 1 through 4. Also, do not rename `index.html` to anything else.
2.  (Optional) Delete the `LICENSE` and `README.md` files. They're nice to have for a GitHub repo but you don't really need them to get your website up and running.
3.  (Opional) Delere the `images` folder. It contains an image that's used in this README file, but is otherwise not needed for your website.
3.  Go to `<yourGithubID>.github.io/<yourRepositoryName>`. You should now see your own content on the website.
4. Keep playing around with the files:
   1. Make your documentation social-media-friendly by editing the Twitter and Facebook metadata tags in the `<head>` section of `_layouts` > `default.html`.
   2. Open a file in the `topics` folder and play with lines 1 to 4 🙂 This part is called `Front Matter` in Jekyll-Liquid parlance. The files in the `topics` folder have only two entries for front matter:
      - `layout`, the value of which in this case is `default`. This tells the build engine to use a file called `default` from the `_layouts` folder to render the page.
      - `title`, the value of which is the text that is displayed as the title of that page on browser tabs.
     
      This front matter is a YAML code block and, for your files to render correctly, should always be placed at the very top of the file. You can specify your own variables here, and call the value of those variables on the page later. For example, you can declare aa array like `hit_list: ['Cruella', 'Villanius', 'Voldemort']` and then pick each item from this array and use it somewhere on the page.
    3. Use your own strings files as data files in `_data`. You can use `.json`, `.csv`, `.tsv`, and `.yml` files. 

## Gotchas

- Ensure that the string IDs in the data files do not contain a period (because Liquid uses the period for referencing). Underscores and hyphens are fine, though.
- You can have both `.html` and `.md` files as your topics but when referencing the `.md` files anywhere else in the doc set (for example, in the ToC), use the `.html` file extension for the file name (because, during the build, Jekyll would've transformed an `xyz.md` file to `xyz.html`).
- Sometimes, the strings themselves include code variables or tokens, the values of which are substituted during runtime. For example, a string like `At {{ timestamp }}, {{ username }} reported an incident at {{ location }}` is rendered on the UI at runtime as `At 12:30 hrs 22-Feb-2066, Skywalker reported an incident at Azbakan`. I haven't yet found a way to handle such strings through Liquid.

## Resources

-  Liquid [introduction](https://shopify.github.io/liquid/tags/comment/)
-  Jekyll [variables](https://jekyllrb.com/docs/variables/) and [includes](https://jekyllrb.com/docs/includes/)
