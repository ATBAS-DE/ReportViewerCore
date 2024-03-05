pipeline {
	agent any

	environment {
		NUGET_API_KEY = credentials('NuGetApiKey')
		NUGET_HOSTED = credentials('NuGetHosted')
	}

	stages {
		stage('publish') {
			steps {
				dir("Microsoft.ReportViewer.WinForms") {
					bat 'dotnet pack --configuration Release --include-symbols --include-source Microsoft.ReportViewer.WinForms.csproj -p:NuspecFile=ReportViewerCore.WinForms.nuspec'
				}
				bat 'dotnet nuget push **/*.nupkg -k %NUGET_API_KEY% -s %NUGET_HOSTED% --skip-duplicate'
			}
		}
	}
}
