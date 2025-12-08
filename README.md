# About me, expressed as a PowerShell script

```powershell
class Candidate {
    [string]      $Name
    [string]      $Gender
    [string[]]    $Pronouns
    [string]      $Country
    [string]      $Province
    [string]      $City
    [string]      $AlmaMater
    [string]      $DiscStyle
    [string]      $MbtiType
    [string[]]    $Traits
    [string[]]    $Interests
    [hashtable[]] $Socials
    [hashtable]   $HasExperienceWith
    [string[]]    $IndustryCertifications
    [string[]]    $RolesInterestedIn

    Candidate() { $this.InterviewCandidate(@{}) }
    Candidate([hashtable]$Properties) { $this.InterviewCandidate($Properties) }

    [void] InterviewCandidate([hashtable]$Properties) {
        foreach ($Property in $Properties.Keys) {
            $this.$Property = $Properties["$($Property)"]
        }
    }

    [string] ToJson() {
        $CandidateAsJson = ($this | ConvertTo-Json -Depth 8 -Compress)
        return $CandidateAsJson
    }
}

$Candidates = [System.Collections.Generic.List[Candidate]]::new()
$Candidates.Add([Candidate]::new(@{
    Name      = "Wouter van den Meulenhof"
    Gender    = "Male"
    Pronouns  = @("He","Him","His")
    Country   = "The Netherlands"
    Province  = "North Brabant"
    City      = "Helmond"
    AlmaMater = "Fontys University of Applied Sciences"
    DiscStyle = "C"
    MbtiType  = "INTJ"
    Traits    = @("Informal", "Curious", "Enthusiastic", "Driven", "Committed")
    Interests = @("Computers","History","Sci-fi","Board Games","LEGO")
    Socials   = @( 
        @{ Name = "LinkedIn"; Url = "https://www.linkedin.com/in/wouter-van-den-meulenhof" },
        @{ Name = "GitHub"; Url = "https://github.com/moulincourt" } 
    )

    HasExperienceWith = @{
        WaysOfWorking    = @("Agile/Scrum","ITIL","GitOps","DevOps")
        CloudServices    = @("Microsoft Azure","Microsoft Entra","Microsoft365")
        Hypervisors      = @("Hyper-V","Proxmox")
        BackupAndRestore = @("Azure Recovery Services","Veeam Backup & Replication")
        OperatingSystems = @("Microsoft Windows (Server)","MacOS","Debian Linux")
        Databases        = @("Microsoft SQL Server","Azure SQL","CosmosDB")
        InfraAsCode      = @("Terraform","Ansible")
        Languages        = @("PowerShell","Python","T-SQL")
        Tools            = @("Azure DevOps","GitHub","Docker","VSCode","Git")
    }

    IndustryCertifications = @(
        "Microsoft Certified: DevOps Engineer Expert",
        "Microsoft Certified: Azure Solutions Architect Expert",
        "Microsoft Certified: Azure Cosmos DB Developer Specialty",
        "Microsoft Certified: Azure Database Administrator Associate",
        "Microsoft Certified: Azure Network Engineer Associate",
        "Microsoft Certified: Azure Security Engineer Associate",
        "Microsoft Certified: Azure Administrator Associate",
        "Microsoft Certified: Windows Server Hybrid Administrator Associate",
        "Microsoft Certified: Azure AI Fundamentals",
        "Microsoft Certified: Azure Data Fundamentals",
        "Microsoft Certified: Azure Fundamentals",
        "HashiCorp Certified: Terraform Associate (expired)",
        "ITIL 4 Foundation"
    )

    RolesInterestedIn = @(
        "Cloud Engineer",
        "Systems Engineer",
        "Database Administrator",
        "Technical Application Manager"
    )
}))

# Login to Azure using this system's managed identity.
Connect-AzAccount -Identity -Subscription "hrsystems-prod"

# Fetch an access token for the Azure SQL service and loop through our list of candidates.
$Token  = (Get-AzAccessToken -ResourceUrl "https://database.windows.net/").Token
foreach ($Candidate in $Candidates) {
    try {
        # Format the candidate's info into a correct query.
        $Name  = $Candidate.Name.Replace("'","''")
        $Json  = $Candidate.ToJson().Replace("'","''")
        $Query = (
            "INSERT INTO Recruitment.Candidates (Name, ProfileJson) " +
            "OUTPUT INSERTED.id "                                     +
            "VALUES(N'$($Name)',N'$($Json)');"
        )


        # Insert the candidate's info into the database.
        $Result = Invoke-Sqlcmd -ServerInstance "sqlsrv-hrsystems-prod-weu.database.windows.net" `
                                -Database "HRSystemsDB"                                          `
                                -AccessToken $Token                                              `
                                -Query $Query                                                    `
        $CandidateId = $Result.Id

        Write-Output "Successfully inserted candidate $($Candidate.Name): $CandidateId"        
    } catch {
        Write-Warning "Failed to insert candidate $($Candidate.Name): $($_.Exception.Message)"
    }
}
```
