# S2 | Prog&Algo: TD07 Graphes

## TD07 Graphes

**Romane MARTEAU--BAZOUNI**

# Exercice 1 (Prise en main)

Commandes tapées :
- ```./TD_Graph_Prog-Algo2.exe extract data/test.osm data/test_extract.graph``` : extrait la carte dans le dossier data
- ```./TD_Graph_Prog-Algo2.exe simplify data/test_extract.graph``` : simplification de la carte extraite
- ```./TD_Graph_Prog-Algo2.exe visualize data/test_extract.graph``` : affichage de la carte simplifiée

# Exercice 2 (Lecture de code)

## Question 1

Les stuctures sont définies dans les fichiers ```.hpp``` appelés ```weightedGraph.hpp``` et ```positionedGraph.hpp```. La structure WeightedGraph stocke une ```unordered_map``` pour définir un graphe pondéré. La structure PositionedGraph stocke, en plus des poids des arêtes, les positions des noeuds.

## Question 2

- **Extraction OSM** : Prend en paramètres le chemin vers un fichier OSM et en extrait les informations sur les noeuds, les liaisons et les voies. Il filtre certaines voies (les bâtiments et les chemins) et construit un ```positionedGraph``` à partir de ces données.


- **Simplification** : Il prend en paramètres un ```positionedGraph``` (dans notre cas, le résultat de l'extraction) et le simplifie. En particulier, il garde le plus grand composant connexe (en maths, sous-groupe qui ne fait partie d'aucun sous-groupe plus grand) ; enlève les petites arêtes ; enlève les noeuds de degré 2 en fonction d'un seuil d'angle ; regroupe les noeuds proches...


- **Visualisation** : Permet l'affichage de la carte grâce à une boucle d'affichage et de la manipuler (zoomer, la fermer...).

## Question 3

5 étapes :


- ```keep_only_largest_connected_component(graph);``` : on ne garde que le plus grand composant connexe (plus grand sous-groupe). Ceci permet de simplifier le graphe en supprimant les noeuds isolés.
- ```remove_small_ending_edge(graph, 10.0);``` : on ne garde pas les arêtes finales les plus petites.
- ```remove_degree_two_nodes_by_angle_threshold(graph, 30);``` : on enlève les noeuds de degré 2 (2 voisins) ayant un angle faible.
- ```group_nodes_by_connection_depth_and_proximity(graph, 10.0, 6);``` : on regroupe les noeuds en cluster, en fonction de leur proximité.
- ```remove_degree_two_nodes_by_angle_threshold(graph, 30);``` : on enlève les noeuds de degré 2 (2 voisins) ayant un angle faible.

Ainsi, ces simplifications permettent d'avoir un graphe avec un minimum de noeuds et d'arêtes. En effet, les noueds sont des clusters de noeuds regroupés.

# Exercice 3 (Dijkstra)