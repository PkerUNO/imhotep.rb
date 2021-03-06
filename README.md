# imhotep.rb

A tool for the K&L Bitesize teams to verify that all images in the migration log are accounted for in the New K&L Product.

The script takes a source URL and a migration log, then scrapes the source URL and all indexs, revision bites and test bites, collecting a list of images it's found. It then goes through each entry in the migration log, checking to see if it found an image for each given PID. It will also check that each image size defined in the migrations log is actually present on the server. It finally outputs a .csv of results.

## Installation

The script requires Ruby and several gems. To check if your machine has Ruby, type in the following in a command line:

    ruby -v

You should see something like:

    ruby 2.0.0p247 (2013-06-27) [i386-mingw32]

As long as you have Ruby 2 or later you should be OK. I haven't tested the script with Ruby 1.8 or 1.9.

If you don't have Ruby or it's outdated, and you're on a Windows machine, go to http://rubyinstaller.org and follow the instructions. Make sure to select the "Add Ruby to PATH" option.

You also need a couple of dependencies, each of which you only ever need to install once. If you have Bundler, run:

    bundle install

Otherwise you can run the following to install the dependencies manually:

    gem install -p http://www-cache.reith.bbc.co.uk:80 roo
    gem install -p http://www-cache.reith.bbc.co.uk:80 fastimage

This should install both roo, necessary to read migration logs, and nokogiri, used to scrape the website.
Fastimage is used to get the image sizes during comparison.

## Usage

For ease of use, place the imhotep.rb script and the migration log in an easy-to-type directory - I'd recommend something like D:\imhotep\ as an example.

Then, inside the command line, run:

    ruby imhotep.rb -u URL -l LOG.XLSX [-g/-p/-b]

- URL is the main index page for the subject you're trying to check (example: http://www.bbc.co.uk/education/subjects/zgm2pv4 but just **subjects/zgm2pv4** will work)
- LOG.XLSX is the migration log to check against. It must be saved in the .xlsx format (example: **nat4_lifeskills_maths_migration.xlsx**)
- **-g** to just check the graphics, **-p** to just check the photos, and **-b** for both graphics and photos - graphics-only is the default
- You can also run "ruby imhotep.rb -h" for inline help.

When the script starts scraping, you will see URLs and hashes appear on the screen - this is just to let you know it's working. The URL shows you which index page it's currently scraping, and a hash represents a recognised image.

When finished, the script generates **results.csv** which contains a list of images it couldn't find, as well as all the images it did, and where it found them.

## Known Issues

- Please ensure the migration log doesn't have empty rows at the end of the file - delete them all before running the script.
- Please ensure the columns are named correctly - the PIDs column should be named "PIDs", not "PID's".

## Why "imhotep"?

Because *Imhotep is invisible*. And sometimes, so are infographics, if you're forced to go through each one by hand! It is mainly a cheap Look Around You joke. Also, if you rotate, move and rearrange the letters you kind of get iWonder...
