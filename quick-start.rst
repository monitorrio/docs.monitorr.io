Quick start
============

Installation
-------------

There are a `couple of packages <https://www.nuget.org/packages?q=Monitorr>`_ for Monitorr available on NuGet.


To install Monitorr into your **ASP.NET application**, type the following command into the Package Manager Console window:

.. code-block:: powershell

   PM> Install-Package monitorr.io


Using NuGet Package Manager
----------------------------

 Right-click on your project in Visual Studio and choose the ``Manage NuGet Packages`` menu item. Search for ``Monitorr`` and install the chosen package:

 .. image:: package-manager.png
    :alt: NuGet Package Manager window

Configuration
--------------

After installing the package, open the Web.config file and paste the LogId created at `Monitorr Admin <https://admin.monitorr.io>`_.

.. image:: webconfig.png
   :alt: Web.config



Manual Logging
--------------

To manually log errors to monitorr.io use the LogToMonitorr() extension and pass the LogId created at `Monitorr Admin <https://admin.monitorr.io>`_ as well as the current HTTP conext.

.. image:: manual_log_dotnet.png
  :alt: LogToMonitorr Extension
