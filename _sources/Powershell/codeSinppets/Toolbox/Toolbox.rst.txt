==================
PowerShell Toolbox
==================

.. index::
   single: PowerShell Toolbox
   single: Powershell Code Snippets; PowerShell Toolbox

.. contents::
    :depth: 3
    :backlinks: top

####

The Toolbox is a collection of shorts code snippets who aimed to achieve a single task at a time.

####

--------------------------------------
Get the the licence product of Windows
--------------------------------------

        .. note:: 
            
            **Windows Licence product**
            
            .. code:: PowerShell
                :number-lines:
                :force:
    
                # Run this command as an administrator
                $(Get-WmiObject -query 'select * from SoftwareLicensingService').OA3xOriginalProductKey
    
            .. raw:: html
    
                <u>Results</u>
    
            .. code:: PowerShell
    
                J7BRJ-xxxx-xxxx-xxxx-xxxx6

####

--------
Weblinks
--------

.. target-notes::