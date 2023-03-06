### Update: the official, correct, non-hacky way to pass parameters is just via execute_params: https://github.com/quarto-dev/quarto-python/blob/main/quarto/render.py

## **Using Quarto for Python: Getting it Installed, Running it From Within Python Using the Quarto Library, and A Hacky Way of Modifying the QMD File From Within Python to ‘Pass’ It Parameters**

### I’m Using Quarto Because I Don’t Like Updating Documents Manually or Building From Scratch With Existing Python Libraries

I first heard about Quarto, a tool for generating a variety of document types including html, Word docs, and PDFs, at a conference for R users. The use case was one that I’ve had – there’s a report you want to generate with updated data so that you don’t have to replace text, tables, and graphs manually.

I do not code in R, I code in Python. But as many of the ads I’ve been served on LinkedIn and Facebook in the past few months have reminded me, Quarto can run on Python as well.

I’ve generated Word documents, PowerPoints, and HTML using existing libraries in Python like [python-docx](https://python-docx.readthedocs.io/en/latest/) and [python-pptx](https://python-pptx.readthedocs.io/en/latest/). It’s not ideal. You have to write a lot of code to generate pretty basic formatting. 

Generally for my use cases, it’s not worth it, and I just generate my figures in Python, copy and paste them into documents, and update text manually. For reports that must run regularly and get updated in a fully-automated way, they’re in HTML – but it would be nice to have a broader set of options for document formats. 

It was with that in mind that I installed Quarto to see if I could get it to run in Python and output some documents. Quarto uses markdown, and I use markdown a little, mainly for writing documentation in Jupyter notebooks.

### My Specific Use Case Involves F-Strings, DataFrames, and Graphs/Figures

1. I want to be able to generate a nicely-formatted document where several things will update based on the data:
    1. Text. I want to be able to use f-strings in Python to update document text.
    2. DataFrames. I want my tables to update.
    3. Graphs/figures. I want to be able to embed my updated matplotlib or Plotly figures.
2. I want to be able to generate documents in Word, PDF, or HTML. 
3. I don't want any code blocks to show in the documents. 

### Some Things Came Up When I Was Getting Started (Or Are Still Coming Up)

Getting started with Quarto was somewhat bumpy in part due to my own lack of reading the documentation, but also because things break with not particularly useful error messages (or no error messages at all). But I was ultimately very happy with the results in terms of how the documents looked, once it got working. 

1. If you want to be able to execute Quarto from the command line using .qmd files  (which is what will contain both your code snippets and your formatting) which contain Python, you need to install [this](https://quarto.org/docs/get-started/). If you want to be able to call Quarto from within Python, you need to also install the [Quarto package on PyPI](https://pypi.org/project/quarto/). If you just install the Quarto package, you will not be able to do anything. 
2. Use a virtual environment. There are a lot of dependencies. When I initially tried to run Quarto, I was prompted to install additional libraries beyond the ones listed [here](https://quarto.org/docs/projects/virtual-environments.html). I froze my dependencies and you see them in my requirements.txt file.
3. You can specify the desired file format in either your .qmd file or in the code that you use to tell Quarto what to do (either from the command line or using the Python quarto library). But if you do both and they’re inconsistent – like, if your .qmd file says you want HTML and your command says you want a docx – you may get some error messages, including from the underlying libraries (like plotly), so it’s not obvious that this is a file format issue.
4. You can generate and work with .qmds either in a text editor or an IDE like Sypder. You just have to save them with a .qmd file extension. 
5. If you specify a filepath within the output_file option within quarto.render() using the Python quarto library, you get an error: “ERROR: --output option cannot specify a relative or absolute path”. But you can specify an output directory in your qmd file [like this](https://quarto.org/docs/reference/projects/core.html). 
6. I think that at one point things were breaking because I was using “ s instead of ‘s. If something isn’t working and you don’t know why, you could try changing those. *Edit: trying to replicate this now, I'm not positive that the issue is actually not just #7 -- that there was code that works for an HTML but not a DOCX, so when my .qmd said "HTML" but I ran it as a docx, it broke, and then when I ran it as HTML, it worked -- but that this wasn't a consistency issue, it was a DOCX breaking issue.* 
7. The promise that the code will nicely generate all of your files across formats– it took some time to get there. There was a point where my DataFrame was rendering in the HTML document and the PDF, but not the Word file. And I could never get a plotly scatterplot to render in either the Word file or the PDF, although it showed up fine in my HTML. After going down a rabbit hole of unsuccessfully trying to use plotly to write out to a .PNG instead so I could just embed that .PNG, and reading stack overflow comments about kaleido (the library plotly uses to save to image files) and virtual environments, I gave up and switched to matplotlib and it worked fine across all three file formats.

### The .QMD File, My Python Code Around Quarto.Render(), And My Hacky Way of Passing Parameters to the .QMD File to Filter My Data/Update the Date

The resource that was the most useful for me for my specific use case was [this blog post](https://www.jumpingrivers.com/blog/quarto-for-python-users/); this .qmd example had the functionality I wanted in terms of f-strings, data frames, and graphs. I copied and modified their qmd file, and my own .qmd file, [meteorites.qmd](https://github.com/abigailhaddad/quarto_with_python/blob/main/qmds/meteorites.qmd), does not add any additional functionality.

However, my [main.py](https://github.com/abigailhaddad/quarto_with_python/blob/main/code/main.py) file does. It imports Quarto and uses the quarto.render() function to output files within Python. I prefer this to running it from the command line, in part because I can more easily add functionality around the Quarto functions. 

For instance, what I really want is a .qmd file that I can pass parameters to. Like if I want to generate a Word file based on filtering my data to a specific date range, and that date range changes, I don’t want to have to manually modify my .qmd file whenever I run it, I want to have Python code that will tell the .qmd file what to do.

I didn’t exactly find a way of doing that well, but by putting all of this in Python, I was able to write a hacky way of doing it – by reading in the .qmd file as a text file and using search and replace on it, and then writing it back out to a separate file which you can then run as your updated .qmd file. 

I’m doing this via a dictionary of terms to search and replace, and you could also put the dictionary somewhere else separate from your code if you wanted to track those alternative parameters via your version control tool, and then the only thing you’re modifying in your .py file is the path to the dictionary containing your parameters – not the Python functions and not the core .qmd file that you’ll keep using. 

In my example, I’m modifying a few pieces of the .qmd file via creating a replacement_dictionary variable and then passing it to my replaceThingsInYourQMD function.

1. I’m modifying the date up top to be today’s date, whenever the code runs, using the Python datetime library.
2. I’m filtering the data differently based on year. (I’m hard-coding that.)

It works and I’m able to generate updated output files without manually changing my .qmd file. 

My Git Repository is [here](https://github.com/abigailhaddad/quarto_with_python/tree/main). 
