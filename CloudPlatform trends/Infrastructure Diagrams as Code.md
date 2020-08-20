## Infrastructure Diagrams as Code

* I usually see “at the beginning of a project” many changes happen and keep updated documentation is hard. Those changes happened because the use of agile methodologies in the software industry has become popular a few years ago. Now it is common to have less documentation than before, but diagrams are still important because they help us to get a quick overview. So, how do you keep updated the diagrams in your repository? Do you now about Diagram as code? Here’s how MinJae Kwon defines it:

### Diagrams
* **Diagrams lets you draw the cloud system architecture using Python code and allows you to track the architecture diagram changes in any version control system.**

* Diagrams currently supports six major providers: **AWS, Azure, GCP, Kubernetes, Alibaba Cloud and Oracle Cloud.** It now also supports On-Premise nodes as well as Programming Languages and Frameworks.

### Now, let’s begin!
* The official page has many [examples](https://diagrams.mingrammer.com/docs/getting-started/examples) of diagrams, but I decided to create one sample just to experiment and share my experience with you. So, see an example below.

Now I will explain the parts that make up this tool:

DIAGRAM: It is the main part and it represents the diagram itself.

name: Diagram name
filename: The output filename, without the extension. If not given, it will be generated from the name.
direction: Data flow direction, default is Left/Right. Options: TB|BT|LR|RL.
curvestyle: Curve bending style default is curved. Options: ortho|curved.
outformat: Output file format, default is png. Options: png|jpg| svg|pdf.
show: Open image after save, default is true.
graph_attr: Provide config attributes.
node_attr: Provide config attributes.
edge_attr: Provide config attributes.
NODE: Node represents a node for a specific component or service.

label: Node label.
attrs: Provide config attributes.
CLUSTER: Likes a group of components or services.

label: Cluster label.
direction: Data flow direction, default is Left/Right. Options: TB|BT|LR|RL.
graph_attr: Provide config attributes.
EDGE: A connection between components or services.

node: Parent node.
forward: Points forward.
reverse: Points backward.
label: Edge label.
color: Edge color.
style: Edge style.
attrs: Provide a config attributes.
If you wanna know how to customize attributes, here is a reference link to Graphviz.

Generate an image diagram.
Here are some instructions to install and configure, but if you prefer I’ve created a docker image to keep it simple.

Using python/Graphviz:

# REQUIREMENT:
#  - Python >= 3.6
#  - Graphviz# using pip
$ pip install diagramspython diagrams/diagram.py
Using docker:

docker run --rm -t -v ~/diagrams:/data -e DIAGRAM_FILE=diagram.py --name diagrams samuelsantos/generate-diagrams-as-code
DIAGRAM_FILE — This variable represents the name of the python file that you create. Remember to define a volume :/data, your diagram will be generated inside this volume and your python diagram needs to be inside this folder volume.

After you execute one of the commands above the image will be generated.

Image for postImage for postImage for post
Image for post
Advice: Use show as false if you are using in a version control system.

Now, if you have resources in one of these clouds: AWS | GCP | Azure | Alibaba | IBM, Cloudiscovery can help you create a diagram based on your resources.

Conclusion
I appreciate this tool because I prefer coding than a draw. We can put it to running in a version control system and generate diagrams in each tag or release. If you have any questions or suggestions, leave a comment or reach out to me.

Thanks for reading!

[Source](https://medium.com/swlh/infrastructure-diagrams-as-code-is-it-possible-b6bbae487f21)
