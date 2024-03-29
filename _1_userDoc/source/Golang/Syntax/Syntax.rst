===================
Détails syntaxiques
===================

.. index::
   single: Go Syntaxe
   single: Go; Go Syntaxe

.. contents::    :depth: 3
    :backlinks: top

####

--------------
Aperçu globale
--------------

:Liens_Web:
    * `Apprendre X en Y minutes`_ : Ensemble de code commentée en français permettant d'avoir un
      apperçu concis de l'ensemble des éléments de syntaxe du language.

.. _`Apprendre X en Y minutes`: https://learnxinyminutes.com/docs/fr-fr/go-fr/

####

------------
Basic Types 
------------

Il y a 17 types de bases et 2 alias :

    * bool

    * string

    * int  int8  int16  int32  int64
      uint uint8 uint16 uint32 uint64 uintptr

      .. note:: 

            **int** et **uint** doivent être utilisés par défaut sauf si une taille spécifique est
            necessaire. **int** et **unint** sont dépendent de la plateforme pour laquelle il sont
            compilé. Il pourrons donc être soit un int/uint32 soit un int/uint64.

    * byte 
    
      .. note:: 

            **byte** est un alias de uint8. Il est utilisé pour représenter un byte de données.

    * float32 float64

    * rune
    
      .. note::
        
            **rune** est un alias de int32. il est utiliser pour représenter un caractère Unicode.

    * complex64 complex128

    #. Literal Value Exemple

        +-----------+-----------------------------------------------------------+
        | Types     | Exemples                                                  |
        +===========+===========================================================+
        | int       | 20, -20.                                                  |
        |           | Values can also be expressed in hex (0x14), octal (0o24), |
        |           | and binary notation (0b0010100).                          |
        +-----------+-----------------------------------------------------------+
        | uint      | There are no unint literals. All literal whole numbers    |
        |           | are treated as int values.                                |
        +-----------+-----------------------------------------------------------+
        | byte      | There are no byte literals. Bytes are typically expressed |
        |           | as integer literals (such as 101) or run literals ('e')   |
        |           | since byte type is an alias for the unint8 type.          |
        +-----------+-----------------------------------------------------------+
        | float64   | 20.2, -20.2, 1.2e10, -1.2e10.                             |
        |           | Values can also be expressed in hex notation (0x2p10),    |
        |           | Altrough the exposant is expressed in decimal digits.     |
        +-----------+-----------------------------------------------------------+
        | bool      | true, false                                               |
        +-----------+-----------------------------------------------------------+
        | string    | "Hello". Character sequences escaped with a backslash are |
        |           | interpreted if the value is enclosed in double quotes     |
        |           | ("Hello\\n"). Escape sequences are not interpreted if the |
        |           | is enclosed backquotes (\`Hello\\n\`).                    |
        +-----------+-----------------------------------------------------------+
        | rune      | \'A\', \'\\n\', \'\\u00A5\', \'€\'.                       |
        |           | Characters glyphs, and escape sequences are enclosed in   |
        |           | single quotes.                                            |
        +-----------+-----------------------------------------------------------+

Conversion entre Basic types
============================

**Go** applique une règle stricte sur les conversions. Toutes les conversions doivent être
spécifiquement définie. Il n'est donc pas possible d'additionner un **int** avec un **float32**

    .. warning::

        **Impossible d'additionner des types différents**

        .. code:: go
            :number-lines:
            :force:
            
            func main() {
                const price int = 275
                const tax float32 = 27.50

                fmt.Println(price + tax)
            }

        .. raw:: html

            <u>Results :</u>

        .. code:: go

            ./prog.go:8:14: invalid operation: price + tax (mismatched types int and float32)

        Les 2 éléments étant de types différent, il n'est pas possible de les additionner

Définission du type
===================

Il y a plusieur façons de définir le type des éléments 

Définission Explicite du type
-----------------------------

    #. Définission Explicite simple

        La définission explicite simple permet de déclarer un unique élément à la fois. Elle
        comprend le mot clef de la déclaration (var, const, func ...) et le type. Un élément peut
        être définie puis initialisé ultérieurement.
        
            .. note:: 
                
                **Définission Explicite Simple**
                
                .. code:: go
                    :number-lines:
                    :force:
        
                    func main() {
                        var price int //La variable est déclarée, mais pas initialisée
                        price = 250   //La variable est initialisée par affectation d'une valeur

                        const tax float64 = 27.50 //La constante est déclarée et initialisée dans une même action

                        var qte int = 1 //La variable est déclarée et initialisée en dans une même action

                        fmt.Printf("'price' type: %T - Value: %v\n", price, price)
                        fmt.Printf("'tax' type: %T - Value: %v\n", tax, tax)
                        fmt.Printf("'qte' type: %T - Value: %v\n", qte, qte)
                    }
        
                .. raw:: html
        
                    <u>Results</u>
        
                .. code:: shell
        
                    'price' type: int - Value: 250
                    'tax' type: float64 - Value: 27.5
                    'qty' type: int - Value: 1

    #. Définission Explicite chainées

        Il est possible de définir plusieurs elément d'un coup si ces éléments sont de même type. Le
        nom du type ne sera alors donné qu'une seule fois.

            .. note:: 
                
                **Définission Explicite Chainée**
                
                .. code:: go
                    :number-lines:
                    :force:
        
                    func main() {
                        var price, qte int = 250, 1 //Les 2 variables sont définie et initialiser en une même action.
                        // N.B : le type 'int' n'est renseigné qu'une seule fois

                        fmt.Printf("'price' type: %T - Value: %v\n", price, price)
                        fmt.Printf("'qte' type: %T - Value: %v\n", qte, qte)
                    }
        
                .. raw:: html
        
                    <u>Results</u>
        
                .. code:: shell
        
                    'price' type: int - Value: 250
                    'qty' type: int - Value: 1

Définission Non-Explicite du type
---------------------------------

[WIP]

####

----------
Constantes
----------

Les constantes se déclarent avec le mot clef **const**. Une constante est une information stocké en
mémoire dont la valeur ne peut pas être modifiée après sa déclaration.

Il y a deux types de déclaration de constantes :

    * Les déclaration Typées

    * Les déclaration non-Typées

C'est déclaration peuvent être effectuées au niveau du module ou à l'interrieur d'une fonction.

Constantes typées
=================

Le type de la constante est définie de façon explicite. Le compilateur appliquera se type sur la
constante dans tous les cas.

        .. note:: 
            
            **Constantes Typées**
            
            .. code:: go
                :number-lines:
                :force:
    
                func main() {
                    const price float32 = 250
                    const tax float32 = 27.50
                    fmt.Printf("'price' type: %T - Value: %v\n", price, price)
                    fmt.Printf("'tax' type: %T - Value: %v\n", tax, tax)
                    fmt.Printf("'price'+'tax' type: %T - Value: %v\n", price+tax, price+tax)
                }
    
            .. raw:: html
    
                <u>Results</u>
    
            .. code:: shell

                'price' type: float32 - Value: 250
                'tax' type: float32 - Value: 27.5
                'price'+'tax' type: float32 - Value: 277.5
            
            Les 2 éléments sont de types float32. Il est donc possible de les additionner.

            voir `Conversion entre Basic types`_


Constantes non-typées
=====================

Le type de la constante n'est pas définie au moment de la déclaration. Le compilateur deduira le
type en fonction de la valeur affecté. Ce type peut être ammené à être redéfinie en fonction du
contexte.

Ce mode d'affectation permet de faire du typage dynamique et donc d'additionner des éléments de
types différents.

        .. note:: 
            
            **Constantes non Typées**
            
            .. code:: go
                :number-lines:
                :force:
    
                func main() {
                    const price = 250
                    const tax = 27.50
                    fmt.Printf("'price' type: %T - Value: %v\n", price, price)
                    fmt.Printf("'tax' type: %T - Value: %v\n", tax, tax)
                    fmt.Printf("'price'+'tax' type: %T - Value: %v\n", price+tax, price+tax)
                }
    
            .. raw:: html
    
                <u>Results</u>
    
            .. code:: shell
    
                'price' type: int - Value: 250
                'tax' type: float64 - Value: 27.5
                'price'+'tax' type: float64 - Value: 277.5

            Ici, le type de 'price' est redéfinie dynamiquement en fonction du contexte. le type
            passe alors de **int** à **float64** pour pouvoir additionner les deux valeur.

####

---------
Variables
---------

[WIP]

####

---------
Accolades
---------

La première accolade doit être positionnée sur la même ligne que l'élément au quel elles
appartient.

Exemple pour une fonction :

    .. hint:: 
        
        **Bonne Syntaxe**
        
        .. code:: go
            :number-lines:
            :force:

            func main() {
                fmt.Println("Hello, world")
            }

        .. raw:: html

            <u>Results</u>

        .. code:: go

            Hello, world



    .. warning:: 
        
        **Mauvaise Syntaxe**
        
        .. code:: go
            :number-lines:
            :force:

            func main ()
            { // <-- L'accolade doit être sur la même ligne que la déclaration de la fonction
                fmt.Println("Hello, world")
            }

        .. raw:: html

            <u>Results</u>

        .. code:: go

            ./prog.go:8:1: syntax error: unexpected semicolon or newline before {
                

####

-------
main.go
-------

Tous les projets doivent avoir un fichier "main.go". C'est le fichier principale du programme. Ce
fichier doit contenir une fonction "main()". C'est cette fonction qui est appellée lors de
l'éxécution du programme.

        .. note:: 
            
            **Minimum code**
            
            .. code:: go
                :number-lines:
                :force:
    
                package main

                func main() {
                    // put some cool code here
                }


####

---------
Fonctions
---------

Une fonction peut être déclarée avec des prototypes plus ou moins complexes en fonction de si la
fonction reçoit des arguments, si elle retourne des arguments et si elle est lié à un struct ou à
un interface.

Forme simple
============

Cette forme ne prend pas d'argument, ne retourne rien et n'est pas liée à un autre élément.

  .. image:: ./images/simpleFunction.svg
        :width: 520 px
        :align: center

####

--------
Weblinks
--------

.. target-notes::

