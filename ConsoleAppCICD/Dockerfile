# Use the official Microsoft .NET SDK image for building the app
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the project file and restore any dependencies (via nuget)
COPY *.csproj ./
RUN dotnet restore

# Copy the entire project and build the app
COPY . ./
RUN dotnet publish -c Release -o /app/publish

# Use the official .NET Runtime image to run the app
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base

# Set the working directory inside the container
WORKDIR /app

# Copy the published app from the previous stage
COPY --from=build /app/publish .

# Expose the port that your app will listen to
EXPOSE 80

# Define the entrypoint for the container
ENTRYPOINT ["dotnet", "ConsoleAppCICD.dll"]
