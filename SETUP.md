# Setup Instructions

## Prerequisites

- .NET 8.0 SDK installed
- GitHub account with a repository
- NuGet.org account (for publishing to NuGet.org)

## Local Testing

1. **Restore dependencies:**
   ```bash
   dotnet restore TestNuGetPackage/TestNuGetPackage.csproj
   ```

2. **Build the project:**
   ```bash
   dotnet build TestNuGetPackage/TestNuGetPackage.csproj --configuration Release
   ```

3. **Create the NuGet package:**
   ```bash
   dotnet pack TestNuGetPackage/TestNuGetPackage.csproj --configuration Release --output ./nupkg
   ```

4. **Test the package locally:**
   ```bash
   # Add a local package source
   dotnet nuget add source ./nupkg --name LocalPackages
   
   # Create a test console app
   dotnet new console -n TestConsumer
   cd TestConsumer
   dotnet add package TestNuGetPackage --version 1.0.0
   ```

## GitHub Actions Setup

### For Publishing to NuGet.org

1. **Get your NuGet API Key:**
   - Go to https://www.nuget.org/account/apikeys
   - Create a new API key with "Push" permission
   - Copy the key

2. **Add the secret to GitHub:**
   - Go to your GitHub repository
   - Navigate to Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `NUGET_API_KEY`
   - Value: [paste your NuGet API key]
   - Click "Add secret"

### For Publishing to GitHub Packages

The `GITHUB_TOKEN` is automatically provided by GitHub Actions, so no additional setup is needed.

However, you need to update the workflow file with your GitHub username:
- Replace `${{ github.repository_owner }}` if needed
- Or update the URL format based on your needs

## Triggering the Workflow

### Manual Trigger
- Go to Actions tab in GitHub
- Select "Build and Publish NuGet Package"
- Click "Run workflow"

### Automatic Trigger (Build Only)
- Push to main/master branch
- Create a pull request to main/master

### Automatic Trigger (Build + Publish)
- Create and push a version tag:
  ```bash
  git tag v1.0.0
  git push origin v1.0.0
  ```

## Updating the Package Version

Before creating a new release:

1. Update the version in `TestNuGetPackage/TestNuGetPackage.csproj`:
   ```xml
   <Version>1.0.1</Version>
   ```

2. Commit the change:
   ```bash
   git add TestNuGetPackage/TestNuGetPackage.csproj
   git commit -m "Bump version to 1.0.1"
   git push
   ```

3. Create a new tag:
   ```bash
   git tag v1.0.1
   git push origin v1.0.1
   ```

## Customization

### Update Package Metadata
Edit `TestNuGetPackage/TestNuGetPackage.csproj`:
- `<PackageId>` - Your package name
- `<Authors>` - Your name
- `<Description>` - Package description
- `<RepositoryUrl>` - Your repository URL

### Change Target Framework
Edit the `<TargetFramework>` or use `<TargetFrameworks>` for multi-targeting:
```xml
<TargetFrameworks>net6.0;net7.0;net8.0</TargetFrameworks>
```

## Troubleshooting

- **Build fails:** Check .NET SDK version matches the workflow
- **Push fails:** Verify API key is correct and has proper permissions
- **Package not found:** Ensure version numbers don't conflict with existing packages
