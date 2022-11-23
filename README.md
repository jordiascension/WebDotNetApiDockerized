-Ejectuar un contendor de .net realizado con la dockerfile de visual studio.
Teniendo en cuenta que ya tenemos creada una imagen llamada azureviewnextwebapi

https://learn.microsoft.com/en-us/aspnet/core/security/docker-https?view=aspnetcore-7.0
dotnet dev-certs https -ep %USERPROFILE%\.aspnet\https\aspnetapp.pfx -p credentials
dotnet dev-certs https --trust

docker build -t azureviewnextwebapi .

docker run -it --rm -e ASPNETCORE_ENVIRONMENT=Development -e ASPNETCORE_URLS=https://+:443;http://+:80 ^
-e ASPNETCORE_Kestrel__Certificates__Default__Password="credentials" ^
-e ASPNETCORE_Kestrel__Certificates__Default__Path=/https/aspnetapp.pfx -v %USERPROFILE%\.aspnet\https:/https/ --name servidor_web -p 80:80 -p 443:443 azureviewnextwebapi 
