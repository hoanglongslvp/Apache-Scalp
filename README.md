Scalp 360! is a fork of nanopony's fork of the GoogleCode-based developed on behalf of BalloonPlanet.com. Our aim is to automate the process of scalping apache logs, sending the results by email.

# Scalp 360!

Scalp! is a log analyzer for the Apache web server that aims to look for security problems developed by Romain Gaucher. The main idea is to look through huge log files and extract the possible attacks that have been sent through HTTP/GET (By default, Apache does not log the HTTP/POST variable).

default_filters.xml is a part of PHP IDS project;

## How it works
Scalp is basically using the regular expression from the PHP-IDS project and matches the lines from the Apache access log file. These regexp has been chosen because of their quality and the top activity of the team maintaining that project.

### How to use
Scalp has a couple of options that may be useful in order to save time when scalping a huge log file or in order to perform a full examination; the default options are almost okay for log files of hundreds of MB.

Edit the config file under scalp/config.py.example with your email server data and save as example/config.py

Current options:
- exhaustive: Won't stop at the first pattern matched, but will test all the patterns
- tough: Will decode a part of potential attacks (this is done to use better the regexp from PHP-IDS in order to - decrease the false-negative rate)
- period: Specify a time-frame to look at, all the rest will be ignored
- sample: Does a random sampling of the log lines in order to look at a certain percentage, this is useful when the user doesn't want to do a full scan of all the log, but just ping it to see if there is some problem...
- attack: Specify what classes of vulnerabilities the tool will look at (eg, look only for XSS, SQL Injection, etc.)

Run or setup the following as a cron task:

    python ./scalp.py -l /var/log/httpd_log -f ./default_filter.xml -o ./scalp-output --email
