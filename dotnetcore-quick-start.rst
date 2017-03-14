.NET Core Quick start
=====================

Installation
-------------

There are a `couple of packages <https://www.nuget.org/packages?q=ElmahBucket>`_ for ElmahBucket available on NuGet.


To install ElmahBucket into your **.NET Core application**, type the following command into the Package Manager Console window:

.. code-block:: powershell

   PM> Install-Package elmahbucket.io.dotnetcore


Using NuGet Package Manager
----------------------------

 Right-click on your project in Visual Studio and choose the ``Manage NuGet Packages`` menu item. Search for ``ElmahBucket`` and install the chosen package:

 .. image:: nuget_sample_1.png
    :alt: NuGet Package Manager window

Configuration
--------------

After installing the package, configure the elmahbucket.io logger in ``Startup.cs`` or anywhere else where the application is being initialized.

.. image:: dotnetcore_init.png
   :alt: .Net Core Configuration
   

Manual Logging
--------------

To manually log errors to elmahbucket.io use the LogToElmahBucket() extension and pass the LogId created at `ElmahBucket Admin <https://admin.elmahbucket.io>`_ as well as the current HTTP conext.

.. image:: manual_log_dotnetcore.png
  :alt: LogToElmahBucket Extension
