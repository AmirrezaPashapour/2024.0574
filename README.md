[![INFORMS Journal on Computing Logo](https://INFORMSJoC.github.io/logos/INFORMS_Journal_on_Computing_Header.jpg)](https://pubsonline.informs.org/journal/ijoc)

# A Quantum Inspired Bi-level Optimization Algorithm for the First Responder Network Design Problem
This archive is distributed in association with the [INFORMS Journal on
Computing](https://pubsonline.informs.org/journal/ijoc) under the [MIT License](LICENSE).

The software and data in this repository are a snapshot of the software and data
that were used in the research reported on in the paper 
[A Quantum Inspired Bi-level Optimization Algorithm for the First Responder Network Design Problem](https://doi.org/10.1287/ijoc.2024.0574) by Anthony Karahalios, Sridhar Tayur, Ananth Tenneti, Amirezza Pashapour, Sibel F. Salman, and Baris Yildiz.

## Cite

To cite the contents of this repository, please cite both the paper and this repo, using their respective DOIs.

https://doi.org/10.1287/ijoc.2024.0574

https://doi.org/10.1287/ijoc.2024.0574.cd

Below is the BibTex for citing this snapshot of the repository.

```
@misc{Karahalios2024,
  author =        {Karahalios, Anthony and Tayur, Sridhar and Tenneti, Ananth and Pashapour, Amirreza and Salman, F. Sibel and Yildiz, Baris},
  publisher =     {INFORMS Journal on Computing},
  title =         {{A Quantum Inspired Bi-level Optimization Algorithm for the First Responder Network Design Problem}},
  year =          {2024},
  doi =           {10.1287/ijoc.2024.0574.cd},
  url =           {https://github.com/INFORMSJoC/2024.0574},
  note =          {Available for download at https://github.com/INFORMSJoC/2024.0574},
}  
```

## Description

The software in this repository is developed to solve the First Responder Network Design Problem (FRNDP) using Graver Augmentation Multi-seeded Algorithm (GAMA) and Branch-and-Bound.

## Building
The code for Bi-level GAMA (GAGA) is in the src directory. This is divided into 3 subdirectories: 
1. code_paths_generation: Path generation for random-graph instances and case-study instances
2. code_random: Graver walk on random-graph instances
3. code_Tgraph: Graver walk on case-study instances

To solve the FRNDP using GAGA, we generate paths and carry out Graver augmentation. The steps are discussed below.

For random graph instances:

a) Path generation: The script to generate paths is code_paths_generation/main_gen_paths_random_instances.py

   i) Example Usage:  

          python main_gen_paths_random_instances.py --nodes_file_cinput='data/instances/random_instances/nodes_30_0.75_0.csv' --edges_file_cinput='data/instances/random_instances/edges_30_0.75_0.csv' --path_save_data_cinput='data/Q-HOPE_output/random_instances/graph_30_0.75_0' --nsamples_cinput=10000 --feas_sols_cinput=True --graver_basis_cinput=True

b) Graver Augmentation: The code is located in code_random. 

   i)  Compilation: 

          g++ -O3 func_cost.cpp func_SR.cpp selfish_routing_leblanc.cpp func_leblanc.cpp main_FR_random_instances.cpp -o ./main_FR_random_instances

   ii) Run: 

          ./main_FR_random_instances --outputdirectory --nodesfile --edgesfile

   iii) Example: 

          ./main_FR_random_instances data/Q-HOPE_output/random_instances/graph_10000SA_30_0.75_0 data/instances/random_instances_reorder/nodes_30_0.75_0.csv data/instances/random_instances_reorder/edges_30_0.75_0.csv


For case study instances:

a) Path generation: The script to generate paths is code_paths_generation/main_gen_paths_Tgraph_instances.py

   i) Example Usage:  

          python main_gen_paths_Tgraph_instances.py --nodes_file_cinput='data/instances/Tgraph_noNorm/nodes_1.csv' --edges_file_cinput='data/instances/Tgraph_noNorm/edges_1.csv' --path_save_data_cinput='data/Q-HOPE_output/Tgraph/graph_10000SA1__1' --feas_sols_cinput=True --graver_basis_cinput=True

b) Graver Augmentation: The code is located in code_random.

   i)  Compilation: 

          g++ -O3 func_cost.cpp func_SR.cpp selfish_routing_leblanc.cpp func_leblanc.cpp main_FR_Tgraph_instances.cpp -o ./main_FR_Tgraph_instances

   ii) Run: 

          ./main_FR_random_instances --outputdirectory --nodesfile --edgesfile --specify_toerance (0: No Tolerance, 1: Tolerance)

   iii) Example: 

          ./main_FR_Tgraph_instances data/Q-HOPE_output/Tgraph/graph_10000SA1__1 data/instances/Tgraph_noNorm/nodes_1.csv data/instances/Tgraph_noNorm/edges_1.csv 0 (no tolerance threshold)

          ./main_FR_Tgraph_instances data/Q-HOPE_output/Tgraph/graph_10000SA1__1 data/instances/Tgraph_noNorm/nodes_1.csv data/instances/Tgraph_noNorm/edges_1.csv 1 (with tolerance threshold)

Branch-and-bound: In Linux, use the Makefile to compile the binary leblanc\_solver

```
make
```

Be sure to make clean before building a different version of the code.

## Scripts
The script run\_instances.sh can be used to run the leblanc\_solver over a directory of instances.

Figures can be generated from the scripts/figs_Tgraph.py. Also outputs the associated Tables.

Tables for the 10, 20 and 30 node random instances can be generated using the scripts/table_rand_instances10node.py and scripts/table_rand_instances.py
