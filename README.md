# docs-as-code

Keep your technical documentation always in sync with UI changes. 

Pull the text of UI labels, hints, error messages, menu options, and so on from code and use them in your documentation as variables, so that when you build your techdoc pages, they are automatically updated with the code changes.

How?

If your techdocs are written in Markdown or HTML, you can use the objects, tags, and filters of the Liquid template language in your doc files, and then build your techdocs with Jekyll (which understands Liquid). So, for example, if your techdoc has something like this:

`To access your tokens, go to {{ site.data.uitext.menu-account }} > {{ site.data.uitext.menu-security }} .`

it'll be rendered like this:

`To access your tokens, go to Account > Security .`

Tomorrow, if your UI changes, and `Account` is renamed to something like `Settings` or `Configuration`, all you'd need to do is to update the UI strings file that holds the mapping between the UI text IDs and the text (for example, a `.csv` or a `.json` file that contains the strings that you send across for translations). The moment you update this UI strings file, and run the Jekyll build, all your techdoc pages get updated automatically.

GitHub also uses the Jekyll rendering engine to handle the repo websites. This means, you can see this concept in use at https://aninditabasu.github.io/docs-as-code/.

To use the Jekyll rendering engine, your directory structure should follow a specific structure. The files in this repo are arranged in that structure, so if you want to experiment with migrating your techdocs to Liquid+Jekyll, feel free to use this repo as a template (or fork it).
