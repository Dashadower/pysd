---
title: 'PySD: System Dynamics Modeling in Python'
tags:
  - Python
  - System Dynamics
  - Vensim
  - Stella
authors:
  - name: Eneko Martin-Martinez^[co-first author]
    orcid: 0000-0002-9213-7818
    affiliation: 1
  - name: Roger Samsó^[co-first author]
    orcid: 0000-0003-0348-3047
    affiliation: 1
  - name: James Houghton
    orcid: #TODO
    affiliation: 2
  - name: Jordi Solé
    orcid: 0000-0002-2371-1652
    affiliation: "1, 3"
affiliations:
 - name: Centre for Ecological Research and Forestry Applications (CREAF)
   index: 1
 - name: Computational Social Science Lab, University of Pennsylvania
   index: 2
 - name: Department of Earth and Ocean Dynamics, Faculty of Earth Sciences, University of Barcelona
   index: 3
date: 20 January 2022
bibliography: paper.bib

---

## Summary

System Dynamics (SD) is a mathematical approach used to describe and simulate the dynamics of complex systems over time. The foundations of the methodology were laid in the 1950s by Professor Jay W. Forrester of the Massachusetts Institute of Technology (MIT) [@Forrester:1971]. The building blocks of SD models are stocks, flows, variables, parameters, and lookup tables. Stocks represent cumulative quantities which take a certain value at each moment in time (integral), and flows are the rates at which those quantities change per unit of time (derivative). Variables express intermediate calculations, parameters set external conditions for the simulation, and lookup tables are single-valued functions that accept another model component as an argument. These components can combine to create feedback loops in which the state of the stock variables feeds back to influence flows in the model. The relationships between these model components can be represented using causal loop diagrams (Figure \ref{fig:CLD}).

![An example Causal Loop Diagram showing how the various components of system dynamics models are visualized by domain-specific modeling environments. \label{fig:CLD}](CLD_example.png)

Since its inception, the SD methodology has been applied in different areas, including manufacturing, energy, climate, population, ecology and economics [@croads:2012;@Moallemi:2021;@FETENEADANE2019212;@harvey:2021]. In the 1990s, the popularity of the methodology gave rise to the development of several visual programming systems for building SD models. These domain-specific modeling environments were widely adopted by the SD community due to their convenient graphical user interfaces (GUIs). Stella&#174; and Vensim&#174; are two of the most popular system dynamics modeling tools, but many others exist (see @wiki:Comparison_of_system_dynamics_software;@sdopentools).

PySD [@pysd:2014] is a Python library that transpiles models built in Stella&#174; or Vensim&#174;'s domain-specific language into Python, allowing the user to load, parametrize and execute SD models, and to take advantage of Python's extensive data-science capabilities. PySD was first released in September 2014 by James Houghton [@houghton_siegel_2015], and has 26 public releases to date, *v2.2.4* the most recent.

The main functional elements of PySD are 1) a set of parsing expression grammars (PEGs) (and their corresponding node visitor classes) to parse models built using Stella&#174; and Vensim&#174; (in *.xmile* and *.mdl* formats, respectively); 2) isomorphic implementations of the most frequently used Stella&#174; and Vensim&#174; built-in functions and other basic operations; 3) a builder, to write the parsed model code in Python and 4) a fordward Euler solver to run the models.

In addition to the aforementioned core functionality, PySD also allows users to import model inputs from external sources (from spreadsheet files), modify model variables at runtime, split models into any number of modules and submodules (corresponding to Vensim&#174; views), isolate parts of a model to be run individually, store intermediate simulation results and resume the simulation from that particular state, and run models using PySD alone (without Stella&#174; or Vensim&#174;). Finally, all these features are made available to the user through a command-line interface.

Despite its maturity, PySD is currently in a very active development phase, and a proof to that is that most of the extra features listed in the paragraph above were implemented in the 14 months that separate releases *v0.11.0* and *v2.2.1*. The roadmap for the next major release (3.0) will focus on cutting down simulation times and on including additional built-in Stella&#174; and Vensim&#174; functions. The most relevant performance-oriented development will be the migration from xarray to numpy to perform array operations, which in addition to the expected overhead reduction will also allow for further potential model optimizations (i.e. JIT compilation). This migration will be facilitated by an even larger development scheduled for the 3.0 release, which corresponds to isolating the parsing process from the building process. This will be achieved by creating an intermediate or abstract model representation (AMR)(Figure \ref{fig:ABSTRACTMODEL}) that will embed all the information contained in the original models, plus additional information such as the order of operations, in pure Python objects. This intermediate AMR will open the door to the development of additional model builders (in Python) to write the output models in any programming language. Furthermore, the intermediate abstract model may encourage the development of new tools to generate and analyze the graphs associated with the models.

![Comparison of the current and upcoming model parsing-building logic in PySD. NOTE: only the Python model builder will be included in release 3.0. \label{fig:ABSTRACTMODEL}](abstract_model.png)

## Statement of need

Stella&#174; and Vensim&#174; are excellent tools for model conceptualization and design using casual loop diagrams. Their solvers are easy to parametrize, efficient (implemented in C and C++) and throughly tested. However, the Python ecosystem offers powerful open-source tools for data visualization, sensitivity analysis, graph theory, machine learning and other data analysis tasks that are unavailable in the domain-specific modeling environments. Most importantly, though models created using Stella&#174; and Vensim&#174; can be exported into text format (*.xmile* and *.mdl*, respectively), users must install propietary software in order to execute the models and visualize the results.

PySD was designed to supplement the capabilities of the domain-specific modeling tools by bringing their outputs into the larger Python data analytics ecosystem. This approach allows users to integrate their models with the most up-to-date analytics tools, and allows the large Stella&#174; and Vensim&#174; user-base to make their models fully open-source and sharable.

PySD is in use by hundreds of modelers and data scientists in academia, industry, and government; and has been used in over two dozen academic publications. The latest improvements to the library have taken place in the context of the European H2020 projects MEDEAS [@medeasproj] and LOCOMOTION [@locomotionproj], in which several authors of the present work participate. The MEDEAS project ended in early 2020, and aimed at developing an Integrated Assessment Model (IAM), named *pymedeas* [@pymedeas:2020;@samso:2020], to analyze different energy transition scenarios under biophysical constraints (e.g. climate change and resource availability). The LOCOMOTION project, which is still ongoing (2019-2023), aims to build a new and more complex IAM, departing from the one developed during the MEDEAS project. In MEDEAS the model was built using Vensim&#174;, and later translated to Python using PySD, and the same approach is being used in the LOCOMOTION project.

## Acknowledgements

This work and part of the development of PySD was supported by the European Union through the funding of the MEDEAS and LOCOMOTION projects under the Horizon 2020 research and innovation programme (grant agreements No 69128 and 821105, respectively).
The authors of this paper would like to acknowledge all contributors from the SD community, which have helped improve PySD and kept the project alive for the 8 years since it was created.

## References
