# Reading List Tools (rltools)
A primitive collection of tools for creating, managing, and viewing reading lists of content stored locally on a system.

## Use Case
An OSX user investigating research topics through google searches who downloads content locally to skim relevent prior work may end up with a collection of pdf documents open in Preview they wish to save as references or for later reading.

## Reading Lists
Simple reading lists stored as flat files in comma separated value (CSV) format can be used to associate the topics and location of such documents. These lists can be automatically created from the current set of files open in Preview windows (and tabs) using the 'rlc' script included in this package.  Once created, a set of documents on a particular topic may be reopened later in the Preview application with the companion 'rlo' script.

## Usage
Clone this git repository or download the scripts and copy them to a folder in your search path.  If that doesn't work, you may need to make them executble if they aren't already (e.g. with `chmod +x rl*`) and or run them explicitly (via `bash <path to script>`) if they aren't in the search path. From the command line use the -h option to see their current usage, for example:

    rlc -h

Usage: rlc 'topic'
  
Create a reading list from documents currently open in an application.  
  
The output is a series of comma separated value (CSV) lines written to standard  
out consisting of a topic tag and absolute path to an open document/file.  
  
Options recognized:  
-h -- Print usage message and exit  
-f -- Append output to named file (default: write to STDOUT)  
-a -- The application name (default: Preview)  
-t -- The document/file type opened by the application (default: '.pdf')  
  
All remaining positional (non-option) parameters are concatenated (joined with  
a blank separator) and used as the reading list topic tag (default: 'ReadLater')  

## Examples
The scripts work by default with the standard output and input streams which may be redirected to or from files.  To see the list of documents that will be saved (with the default topic 'ReadLater') run the command:

    rlc
which will output a line containing the topic 'ReadLater' and the path for each of the pdf files currently open in the Preview application.  You can assign your own custom topic from the command line.  There is no need to escape spaces in topic names, all the words are concatenated into a single tag (joined with spaces).

    rlc Your Topic Name
By redirecting the output from the script, reading lists can be saved in a file.

    rlc Your Topic Name > yourtopicname.csv

Will create (or overwrite) the file 'yourtopicname.csv'.  Append the contents to an existing file with the `>>` redirection operator.  Alternatively, a file name may be specified with the `-f` command line option.

    rlc -f anothertopic.txt Another Topic Name

For safety, output will be appended to any contents already in the file. Reading list files can have any file extension. When appending to an existing file, documents on different topics may be combined.  The same document may also be stored under different topics. The scripts don't impose any requirement on how reading lists are managed, supporting both single or multiple lists and single or multi-topic lists.

The files in a reading list my be reopened with the `rlo` command (`rlo -h` for usage instructions).
    rlo < readinglist.csv

will open all the documents previously saved in the file readinglist.csv with any topic tag.  Documents on a specific topic can be opened by specifying the topic name on the command line.
    rlo -f computervision.lst Segmentation

would open only the documents tagged 'Segmentation' in the computervisdion.lst reading list.