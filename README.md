# Big Data Analytics
Work material for parts of a course "Applied Computing and Big Data" offered by Blekinge Institute of Technology.

We are using the [Qualitas Corpus](http://qualitascorpus.com/) as a starting point for some fun very-nearly-big-data analysis.

Documentation and step-by-step instructions for this part of the course is found in the [Documentation](Documentation) directory.

## About the Course
The course Applied Cloud Computing and Big Data is a 7.5 ECTS course offered by Blekinge Institute of Technology. The course is organised around three themes, and all three themes must be completed to complete the course:

- Cloud Provisioning and Deployment
- The Business Case for Cloud Computing
- Big Data Analytics

The course is divided across two source code repositories:

- https://github.com/mickesv/ProvisioningDeployment.git contains the instructions and source code for the Cloud Provisioning and Deployment, and the Business Case for Cloud Computing parts of the course.
- https://github.com/mickesv/BigDataAnalytics.git contains the instructions and source code for the Big Data Analytics part of the course.

## Apply
If you wish to apply for the course, please visit [UniversityAdmissions](https://www.universityadmissions.se/intl/start) and search for "Applied Cloud Computing and Big Data".

The Code Stream Clone Detector consists of two parts, a CodeStreamGenerator and a CodeStreamConsumer. Below, a brief overview of each is provided.

CodeStreamGenerator The generator is just a placeholder for whencesoever new files may be submitted to the clone detector for inspection. This may, for example, be through a website where users submit suspicious code, or via a hook in the configuration management system that automatically send all commits for clone detection. The CodeStreamGenerator expects the previously generated qc-volume to be mounted under /QualitasCorpus so that it has some code to “generate”. You could, of course, mount any code repository in this place, and CodeStreamGenerator would be none the wiser.

The source code for the CodeStreamGenerator is found under Containers/CodeStreamGenerator/. It consists of a Dockerfile, a bash script, and two test files that will be sent first if you give the TEST flag to the container. Please take a moment to study the Dockerfile and the bash script so you understand what they do.

CodeStreamConsumer The consumer is a node.js / express.js app, the source code of which is found under Containers/CodeStreamConsumer/ , that waits for a HTTP POST request with a file in it. Each file is processed in turn using the processFile() function, clones are detected, and statistics are collected. Opening a web browser to http://localhost:8080 (Assuming you’ve instructed docker to forward port 8080 on the host to port 3000 in the CodeStreamConsumer container) displays the time it took to process the last file, the code clones found so far, and the names of the thus far processed files.

In the src directory, you will find a small set of files:

$ tree
.
├── CloneDetector.js # This is the actual Clone Detector, discussed further below
├── Clone.js         # The Clone class represents one identified Clone
├── CloneStorage.js  # A Singleton Class to keep track of already identified Clones
├── FileStorage.js   # A Singleton Class to keep track of already processed files
├── index.js         # Start file for the system.
# Sets up the express app and contains
# the ~processFile()~ function.
├── SourceLine.js    # The SourceLine class represent a single line
# (including its original line number) in a file.
└── Timer.js         # This class is used to start and stop timers as needed.

The processFiles() function follows the previously outlined overall process for code detection, with pre-processing, transformation, match detection, post-processing, and storage. Primarily, it is the CloneDetector class that implements these steps.

In the CodeStreamConsumer a file is the central concept through all of these steps. Each processing step may add new fields to the file object. Just before storage, it will contain the following fields:

file.name       // Full path and name of the original file.
file.contents   // Original contents as a single string.
file.lines      // An array of SourceLines.
// These are generated by CloneDetector::#filterLines(),
// which replaces empty lines and comment lines with ''
// so they can be easily cleared later.
file.chunks     // An array of Chunks, which are just arrays of
// SourceLines, each having the length CHUNKSIZE.
file.instances  // An array of Clones. The processing steps will
// refine this list so that only true and
// as-long-as-possible Clones remain.
Tasks With these introductions out of the way, it is time to actually fix and run the application.

Generate images for the generator and the consumer, tag them csgenerator and csconsumer, respectively.
Start the application using docker compose with the given stream-of-code.yaml . You may wish to modify the DELAY to something bigger during your first tests so you can see what is going on. You will also notice that the cs-consumer container introduces a bind-mount to the source code of the app so that you can edit the code locally and it will restart automatically.
Study the source code of the CodeStreamConsumer so that you understand it. You will notice that there are two implementation tasks, identified by TODO statements in the code.
The first task is to complete the implementation of the CloneDetector. The smallest possible edit for you is to implement the three methods as suggested, but feel free to be more creative here.
The second task is to add a new landing page in index.js for more detailed timing statistics (not just data on the last processed file). Your own creativity sets the boundaries here, but it is useful to be able to see trends over time for how long it takes to process each new file. You may also wish to normalise the processing time for each file with the number of lines it contains. Make use of the test files A.java and B.java to see if you are able to correctly identify clones (feel free to write a new CodeStreamGenerator that just send these two files on repeat).
Once you are satisfied with your implementation, run the app for a longer period of time so you can get some proper statistics out of it. Make note of what happens, when it happens, and try to reason about causes and remedies.
Summary We have now:

Created and used a docker image/container to fetch a very-nearly-Big-Data repository of source codes, i.e. the Qualitas Corpus.
Stored the QualitasCorpus in a docker volume, qc-volume, for use in subsequent steps
Created a docker image to simulate source code being generated in a continuous stream.
Created a node.js app to consume this stream and look for code clones in any of the previously submitted files.