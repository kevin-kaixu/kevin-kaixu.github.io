*** Source code of facade structure analysis ***

** Description:
This program performs hierarchical structure analysis over the box pattern of a 2D facade image. It takes as input the box pattern of the facade elements and outputs a hierarchical decomposition tree for the facade structure. The hierarchical representation can be seen as a generative model of the input facade structure. Applications of such a representation include structure-aware facade retrieval, editing, and retargeting.

** Components:
* Given a box pattern, compute its Integral Symmetry (IS). IS is a continuous measure of the degree of symmetry
for given a discrete box pattern.
* Compute the optimal hierarchical decomposition tree for an input facade strcutre represented as box pattern using Genetic Algorithm (GA).

** Compile
* We provide the Visual Studio C++ 9.0 project.
* You may need to install QT (later than v4.0) to compile the project
* We utilize Matthew's Genetic Algorithms Library (GALib) (lancet.mit.edu/ga/) for the implementation of GA.

** Usage
* Unzip the package, you will see a VC9.0 solution file and four folders. /AsymAnalysis contains the source code. /bin is where the binary is output. /input is where the test data located. /output is where the results are output
* Put the input box pattern file under /input/tag/, e.g., fac(0).txt
* To run the program, open cmd.exe, cd to /bin/release, then type: AsymAnalysis <input.txt>, e.g., AsymAnalysis fac(0).txt
* After the running is done, you can check out the output: a data file of the hierarchy under /output/hist and a visualized hierarchy rendered as an SVG vetor graph under /output/svg.

** Notes
* For the test data, the box petterns of facade elements are obtained using our Interactive Box Abstraction program (see paper for details). It is an independent program which has not been integrated into the analysis program yet. You can either choose to code up your own or ask for our program via email.
* For more technical questions regarding the code/algorithm, please send email to Kevin Xu (kevin [DOT] kai [DOT] xu [AT] gmail.com)

** Citation
If you use any part of this source code, please cite the following paper:
Hao Zhang, Kai Xu, Wei Jiang, Jinjie Lin, Daniel Cohen-Or and Baoquan Chen. Layered Analysis of Irregular Facades via Symmetry Maximization. ACM Transactions on Graphics (SIGGRAPH 2013), 32(4).
