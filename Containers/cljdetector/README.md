# cljdetector

TODO Answer the following questions:

Are you able to process the entire Qualitas Corpus? If not, what are the main issues (think in terms of data processing and storage) that causes the cljDetector to fail? How may you modify the application to avoid these issues?
Please upload a report of your collected statistics and your analysis thereof. The report shall contain summaries of the collected data, along with answers to the following questions. Please discuss your answers and try to find reasons for why you are getting these results. Are there, for example, any particular characteristica in way the analytics is undertaken or the particular implementation/choice of tools/database that may cause or influence these results and trends?
Is the time to generate chunks constant or does it vary with the number of already generated chunks? Please explain with the help of the implemented algoritm why this is an expected result (or why it is not expected).
Is the time to generate clone candidates constant or does it vary with the number of already generated candidates? Please explain with the help of the implemented algoritm why this is an expected result (or why it is not expected).
Is the time to expand clone candidates constant or does it vary with the number of already expanded clones or the number of remaining candidates? Please explain with the help of the implemented algoritm why this is an expected result (or why it is not expected).
What is the average clone size? How can this be used to predict progress during the expansion phase?
What is the average number of chunks per file? How can this be used to predict progress during the read/chunkify/identify candidates stages?
Please make a sample of the raw data of your statistics accessible (either as an appendix to your report or via a linked web page). The first 100-odd lines of statistics is sufficient.
Please upload your code for the modified cljDetector and your MonitorTool (zip the whole folders with the Containers. Please remember to also include the yaml-file used to start your application). Please highlight any modifications you have made in cljDetector to make it easier for us to review your submission.
Once delivered, a meeting may be scheduled where you are expected to run and explain your application and its deployment. Be prepared to answer questions about:

Your modifications to cljDetector
Your implementation of your MonitorTool
The collected statistics and what they may imply
Possible future improvements
There is a Quiz on Canvas where you can submit your article summaries and answers to the questions.

## Installation

Download from http://example.com/FIXME.

## Usage

FIXME: explanation

    $ java -jar cljdetector-0.1.0-standalone.jar [args]

## Options

FIXME: listing of options this app accepts.

## Examples

...

### Bugs

...

### Any Other Sections
### That You Think
### Might be Useful

## License

Copyright © 2023 FIXME

This program and the accompanying materials are made available under the
terms of the Eclipse Public License 2.0 which is available at
http://www.eclipse.org/legal/epl-2.0.

This Source Code may also be made available under the following Secondary
Licenses when the conditions for such availability set forth in the Eclipse
Public License, v. 2.0 are satisfied: GNU General Public License as published by
the Free Software Foundation, either version 2 of the License, or (at your
option) any later version, with the GNU Classpath Exception which is available
at https://www.gnu.org/software/classpath/license.html.
