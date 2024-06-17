name: Build and Test .NET Application

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up .NET
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: '7.0.x' # Specify the .NET version you are using

    - name: Restore dependencies
      run: dotnet restore

    - name: Build the application
      run: dotnet build --configuration Release --no-restore

    - name: Run tests
      run: dotnet test --no-build --verbosity normal
