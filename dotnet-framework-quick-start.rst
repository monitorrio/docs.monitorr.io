.NET Framework Quick Start
============

Installation
-------------

.NET Framework package for `monitorr.io` is available on NuGet `<https://www.nuget.org/packages?q=Monitorr>`_ .
It uses the popular open source project ELMAH `<https://elmah.github.io/>`_ to log application-wide errors without any additional configuration from the developer side.


To install `monitorr.io` into your **.NET Web application**, type the following command into the Package Manager Console window:

.. code-block:: powershell

   PM> Install-Package monitorr.io


Using NuGet Package Manager
----------------------------

 Right-click on your project in Visual Studio and choose the ``Manage NuGet Packages`` menu item. Search for ``Monitor`` and install the `monitorr.io` latest package:

 .. image:: images/package-manager.png
    :alt: NuGet Package Manager window

Configuration
--------------
After the monitorr.io nuget package has been installed you will see a windows prompting for Log Id.
In order for you application to start logging errors, you will need to signup and login to `https://admin.monitorr.io <https://admin.monitorr.io>`_ dashboard and create a log there.

To get the Log Id,  go into Log settings tab and copy the Log Id.

Manual Logging
--------------

You can manually log errors in you application by using the ``.Monitor()`` extension method on the exception itself and by passing the current Context.

.. code-block:: C#

    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";

        try
        {
            RedirectToAction("NotFound");
        }
        catch (WebException ex)
        {
            ex.Monitor(System.Web.HttpContext.Current);
        }
        return View();
    }

A dictionary of string key value pairs can be passed to the  ``Monitor()`` extension to add any additional custom messages for more granular logging.

.. code-block:: C#

  public ActionResult Contact()
  {
      ViewBag.Message = "Your contact page.";

      try
      {
          RedirectToAction("NotFound");
      }
      catch (WebException ex)
      {
          var data = new Dictionary<string, string>
          {
              { "Type", "redirect error"},
              { "Message", "My custom message"}
          };

          ex.Monitor(System.Web.HttpContext.Current, data);
      }
      return View();
  }
