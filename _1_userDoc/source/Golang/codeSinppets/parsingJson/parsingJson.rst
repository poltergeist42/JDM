============
Parsing Json
============

.. index::
   single: Snippets json
   single: Go; Snippets json

.. contents::
    :depth: 3
    :backlinks: top

####

--------------------------------
parsing json : unstructured json
--------------------------------

Un json non structuré n'a pas forcément la même clé principale contrairement à un json structuré
qui comprend toujours les mêmes clés. Il est donc important de pouvoir parcourir le json de façon
dynamique.

Json Structuré
--------------

    .. code:: json

        {
            "name": "merlin",
            "age": 1000,
            "metiers": "enchanteur"
        },
        {   "name": "Arthur",
            "age": 20,
            "metier": "roi"
        }

Json Non structuré
------------------

    .. code:: json

        {
            "merlin": {
                "age": 1000,
                "metier": "enchanteur"
            },
            "Arthur": {
                "age": 20,
                "metier": "roi"
            }
        }

Json Interne
============

Dans ce Snippet, les données json son fournies dirrectement dans le code au travers d'une variable
interne.

    #. On commence par importer les bibliothèques

       Seule la bibliothèque "encoding/json" est nécéssaire. la bibliothèque "fmt" n'est utiliée que
       pour l'affichage.

        .. code:: Go

            package main

            import (
                "encoding/json"
                "fmt"
            )

    #. On définit ensuite un struct qui sera utilisé pour la mise en forme des données extraites du
       json.

       Puisque tous les éléments d'un struct doivent être publique, donc commencer par une Majuscule,
       il faut établir une correspondance entre les membres du struct et les clés du json.

       Cette correspondence s'établie en ajoutant : `json:"Nom_de_la_clef"` à la suite de la
       déclaration du membre.

        .. code:: Go

            type JsonStruct struct {
                Path    string   `json:"path"`
                Exclude []string `json:"exclude"`
            }

    #. Json Data

       Les données Json son fournie manuellement dans une variable.

        .. code:: Go

            // jsonData from a variable
            var jsonData = `{
                    "Dropbox": {
                        "path": "/home/polter/Dropbox/WEB/atelier/project/_3_software/Atelier/",
                            "exclude": ["node_modules/",".gitignore", "build/"]
                    },
                    "Polux": {
                        "path":"/home/polter/dev/Atelier/",
                        "exclude": []
                    },
                    "Minux": {
                        "path":"/home/polter/dev/Atelier/",
                        "exclude": []
                        },
                    "Labux": {
                        "path":"",
                        "exclude": []
                    }
                }`


    #. Fonction 'main'

       Ici, tout le traitement s'effectue, par facilité, dans la fonction 'main'. Les best practices
       étant au contraire de travailler le plus possible avec des fonctions et des modules pour que
       la fonction 'main' soit le plus simple possible et effectue le moins possible de traitement
       direct.

       .. code:: Go

            func main() {
                // jsonData from a variable

    #. Création d'un dictionnaire de struct (map[string]struct{})

       "map" permet de créer un dictionnaire. C'est à dire de réunir un ensemble de données sous la
       forme Clef / Valeur. 
       
       .. code:: Go

                // Creation of a 'map' (Dictionary) of type 'JsonStruct'
                var config map[string]JsonStruct

       Ici, le type de clef attendue est "string" le dictionnaire lui même est de type "JsonStruct".

                // Unmarshal the json data and send it to the adress (&) of of the map 'config'
                // The json Data must be provided as a slice of byte
                json.Unmarshal([]byte(jsonData), &config)

                for key, _ := range config {
                    fmt.Println("\n/**********/")
                    fmt.Println("key in 'config': ", key)

                    if _, ok := config[key]; ok {
                        fmt.Printf("\nAffichage du 'Path' de %v: %v\n", key, config[key].Path)

                        if isNotEmpty := config[key].Exclude; len(isNotEmpty) != 0 {
                            fmt.Println("\nParcours des elements exclus:")
                            for _, exclude := range config[key].Exclude {
                                fmt.Println(exclude)
                            }
                        }
                    }

                }

            }


####

--------
Weblinks
--------

.. target-notes::