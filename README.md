# Sela-Week3-IIS-app
# ASP.NET Core Web App running on IIS 
*Building steps:*
1. Open Visual Studeio and create new ASP.NET Core Web App
2. Add “Newtonsoft.Json” by Tools -> NuGet Package Manager -> Manage NuGet Packages for solution
3. After rebuilding the solution, the following will be added to the .csproj file:
    ```sh
    <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="13.0.1" />
    </ItemGroup>
4. After building, your bin folder of the prject is populated and after publishing, the bin\Release\netcoreapp3.1\publish\ holds all the files to be copied to your server

*Configuring your IIS steps:*
1. Open Server Manager and click Manage > Add Roles and Features. Click Next.
Select Role-based or feature-based installation and click Next.
Select the appropriate server. The local server is selected by default. Click Next.
Enable Web Server (IIS) and click Next.
No additional features are necessary to install the Web Adaptor, so click Next.
On the Web Server Role (IIS) dialog box, click Next.
On the Select role services dialog box, verify that the web server components listed in the next section are enabled. Click Next.
Verify that your settings are correct and click Install.
When the installation completes, click Close to exit the wizard.
2. Create a new app pool
3. Right click on site and a new site. Set the port as requested (5100) and set teh path to C:\inetpub\wwwroot\{your folder}
1. Copy your files from the local publish folder to the folder created above.
    * Tip: if you get access denied for copying directly to the wwwroot folder from your local fs to the remote desktop, copy to My Documents folder and then copy from there.
4. Browse the app from the IIS manager: http://localhost:5100/
    * If you're browser prompts for "Content From The Website Listed Below Is Being Blocked.”, check a simple solution [here](https://docs.microsoft.com/en-us/archive/blogs/webtopics/troubleshooting-http-500-19-errors-in-iis-7).
5. If you get  HTTP 500.19 Error (The requested page cannot be accessed because the related configuration data for the page is invalid.
), you can check the **event viewer** for this error:
        Could not find 'aspnetcorev2_inprocess.dll'. Exception message:
        It was not possible to find any compatible framework version
        The framework 'Microsoft.AspNetCore.App', version '3.1.0' (x64) was not found.
        The following frameworks were found:
              6.0.2 at [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
        You can resolve the problem by installing the specified framework and/or SDK.
        The specified framework can be found at:
          https://aka.ms/dotnet-core-applaunch?framework=Microsoft.AspNetCore.App&framework_version=3.1.0&arch=x64&rid=win10-x64
  1. Download and install the execitable

*Open your firewall for the requested port:*
1. Open Firewall, add new rule, select port, TCP and state specific port 5100, the rest are defaults. You can follow the instructions [here](https://docs.microsoft.com/en-us/sql/reporting-services/report-server/configure-a-firewall-for-report-server-access?view=sql-server-ver15)
1. Give a name to the rule, so you can identify it easily
1. Open your local browser with the {IP of your machine}:5100
1. You made it!

