{\rtf1\ansi\ansicpg1252\cocoartf2865
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
{\*\listtable{\list\listtemplateid1\listhybrid{\listlevel\levelnfc23\levelnfcn23\leveljc0\leveljcn0\levelfollow0\levelstartat1\levelspace360\levelindent0{\*\levelmarker \{disc\}}{\leveltext\leveltemplateid1\'01\uc0\u8226 ;}{\levelnumbers;}\fi-360\li720\lin720 }{\listname ;}\listid1}}
{\*\listoverridetable{\listoverride\listid1\listoverridecount0\ls1}}
\paperw11900\paperh16840\margl1440\margr1440\vieww29200\viewh15760\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0  
\fs36 Grover's Algorithm using Qiskit\

\fs24 \
Overview:\
This project demonstrates Grover\'92s Quantum Search Algorithm using Qiskit and Qiskit Aer simulators.  \
It was developed as part of my Quantum Computing Internship to explore how quantum computers can achieve faster search in unsorted datasets.\
\
\
Technologies Used:\
\pard\tx220\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\li720\fi-720\pardirnatural\partightenfactor0
\ls1\ilvl0\cf0 {\listtext	\uc0\u8226 	}Python  \
{\listtext	\uc0\u8226 	}Qiskit  \
{\listtext	\uc0\u8226 	}Qiskit Aer  \
{\listtext	\uc0\u8226 	}Matplotlib  \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf0 \
\
Algorithm Explanation\
Grover\'92s Algorithm is a quantum algorithm that finds a marked item from an unsorted dataset in only O(\uc0\u8730 N) time giving a quadratic speedup over classical algorithms.\
\
Steps:\
1. Initialize qubits into superposition using Hadamard gates.  \
2. Apply the Oracle that marks the target state (`|11\uc0\u10217 ` in this case).  \
3. Apply the Diffusion Operator (inversion about the mean).  \
4. Measure the qubits \'97 the marked state appears with the highest probability.\
\
\
\
Code Summary\
\
from qiskit import QuantumCircuit, transpile\
from qiskit_aer import Aer\
\
# Oracle for |11>\
oracle = QuantumCircuit(2)\
oracle.cz(0, 1)\
\
# Diffusion operator\
diffuser = QuantumCircuit(2)\
diffuser.h([0, 1])\
diffuser.x([0, 1])\
diffuser.h(1)\
diffuser.cx(0, 1)\
diffuser.h(1)\
diffuser.x([0, 1])\
diffuser.h([0, 1])\
\
Full Grover circuit\
grover = QuantumCircuit(2, 2)\
grover.h([0, 1])\
grover.append(oracle, [0, 1])\
grover.append(diffuser, [0, 1])\
grover.measure([0, 1], [0, 1])\
\
Run simulation\
counts = Aer.get_backend("qasm_simulator").run(\
    transpile(grover, Aer.get_backend("qasm_simulator")),\
    shots=1024\
).result().get_counts()\
\
plot_histogram(counts)\
print(grover.draw())\
}
