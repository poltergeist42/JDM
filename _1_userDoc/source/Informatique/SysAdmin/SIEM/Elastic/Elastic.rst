================
Elastic / Kibana
================

.. index::
   single: Elastic / Kibana
   single: SIEM; Elastic / Kibana

.. contents::
    :depth: 3
    :backlinks: top

####

    .. note:: 
        
        **Liens Web**

        * `Elastic documentation`_
        
.. _`Elastic documentation`: https://www.elastic.co/guide/index.html


Elastic is a suite of software for distributed search and data analysis.

It includes the following components:

    * **Elasticsearch**: a distributed search and data analysis engine based on
      Apache Lucene.

    * **Kibana**: a web interface for visualizing and exploring data indexed in
      Elasticsearch.

    * **Logstash**: a tool for collecting, aggregating, and transforming data before indexing it in
      Elasticsearch.

    * **Beats**: lightweight agents for sending data to Logstash or Elasticsearch.

Kibana is the graphical user interface of the Elastic suite. It allows you to visualize data
indexed in Elasticsearch in the form of graphs, tables, and maps. Kibana also offers advanced
search and filtering capabilities for exploring data.

The Elastic suite is widely used in Security Information and Event Management (SIEM) environments
to collect, analyze, and visualize security event logs from various sources, such as firewalls,
intrusion detection systems, and servers.

####

--------------------------
Export / import dashboard 
--------------------------

    #. Identifying the dashboard's name to export from the Dashboard view.

        .. note:: 
            
            **Dashboard view**
    
            *Analitytics* > **Dashboard**

            copy the name of the dashboard to export.

                .. image:: images/copyDashboardName.png
                   :width: 350 px
                   :align: center

    
    #. Click on the **Management** menu from the hamburger menu.

        .. note:: 
            
            **Management menu**
    
            .. image:: images/homeManagement.png
                :width: 350 px
                :align: center

       The full menu of the **Management** section will be displayed.


    #. Click on the *Kibana* > **Saved Objects** menu.


    #. Paste the name of the dashboard into the search field and hit enter.
    
    #. Select the object from the list and click on the **Export** button.

        .. note:: 
            
            **Select the object**
    
            .. image:: images/selectObectToexport.png
                :width: 350 px
                :align: center
    


####

--------
Weblinks
--------

.. target-notes::