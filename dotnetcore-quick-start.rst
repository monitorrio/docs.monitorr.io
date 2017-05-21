.NET Core Quick start
=====================

Installation
-------------

.NET Core package for `monitorr.io` is available on NuGet `<https://www.nuget.org/packages?q=Monitorr>`_ .

To install Monitorr into your **.NET Core application**, type the following command into the Package Manager Console window:

.. code-block:: powershell

   PM> Install-Package monitorr.io.dotnetcore


Using NuGet Package Manager
----------------------------

 Right-click on your project in Visual Studio and choose the ``Manage NuGet Packages`` menu item. Search for ``Monitorr`` and install the chosen package:

 .. image:: images/package-manager.png
    :alt: NuGet Package Manager window

Configuration
--------------

After installing the package, configure the monitorr.io logger in ``Startup.cs`` or anywhere else where the application is being initialized.

.. code-block:: C#

    public async void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory, DatabaseInitializer initializer)
    {
        loggerFactory.AddConsole(Configuration.GetSection("Logging"));
        loggerFactory.AddDebug();
        var logPath = Path.Combine(env.WebRootPath, "Logs/app-log-{Date}.txt");
        loggerFactory.AddFile(logPath);


       app.UseMonitorr(new Guid("d46d3856-4f88-4ebc-804d-8e592a9dad55"));

       app.UseCors("CorsPolicy");

       app.UseIdentity();

       ConfigureAuth(app);

       app.UseMvc(routes => { routes.MapRoute(name: "default", template: "{controller=Home}/{action=Index}/{id?}"); });



       await initializer.SeedAsync();
    }

Manual Logging
--------------

To manually log errors to monitorr.io use the Monitorr() extension and pass the LogId created at `Monitorr Admin <https://admin.monitorr.io>`_ as well as the current HTTP context.

.. code-block:: C#

    public IActionResult GenerateException()
    {
        try
        {
            var i = 0;
            var result = 12 / i;
        }
        catch (Exception e)
        {
            e.Monitor(new Guid("d46d3856-4f88-4ebc-804d-8e592a9dad55"), HttpContext);
        }
        return Ok();
    }

A dictionary of string key value pairs can be passed to the  ``Monitor()`` extension to add any additional custom messages for more granular logging.

.. code-block:: C#

    public IActionResult GenerateException()
    {
        try
        {
            var i = 0;
            var result = 12 / i;
        }
        catch (Exception e)
        {
            var data = new Dictionary<string, string>
            {
                { "Type", "custom logged error"},
                { "Message", "My custom message"}
            };
            e.Monitor(new Guid("d46d3856-4f88-4ebc-804d-8e592a9dad55"), HttpContext, data);
        }
        return Ok();
    }
