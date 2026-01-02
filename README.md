```PowerShell
class Engineer {
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
    [hashtable[]] $HasExperienceWith
    [string[]]    $IndustryCertifications
    [string[]]    $RolesInterestedIn

    Engineer() { $this.InterviewEngineer(@{}) }
    Engineer([hashtable]$Properties) { $this.InterviewEngineer($Properties) }

    [void] InterviewEngineer([hashtable]$Properties) {
        foreach ($Property in $Properties.Keys) {
            $this.$Property = $Properties["$($Property)"]
        }
    }

    [string] ToJson() {
        $EngineerAsJson = ($this | ConvertTo-Json -Depth 8 -Compress)
        return $EngineerAsJson
    }
}

$Team = @()
$Team +=[Engineer]::new(@{
    Name      = "Wouter van den Meulenhof"
    Gender    = "Male"
    Pronouns  = @("He","Him","His")
    Country   = "The Netherlands"
    Province  = "North Brabant"
    City      = "Helmond"
    AlmaMater = "Fontys University of Applied Sciences"
    DiscStyle = "C"
    MbtiType  = "INTJ"
    Traits    = @("Informal", "Curious", "Enthusiastic", "Driven")
    Interests = @("Computers","History","Sci-fi","Board Games","LEGO")
    Socials   = @( 
        @{ Name = "LinkedIn"; Url = "https://www.linkedin.com/in/wouter-van-den-meulenhof" },
        @{ Name = "GitHub"; Url = "https://github.com/moulincourt" } 
    )

    HasExperienceWith = @(
        @{ Category = "WaysOfWorking"; Items = @("Agile/Scrum","ITIL","GitOps","DevOps") },
        @{ Category = "IdentityAndAccess";  Items = @("Microsoft Entra","Active Directory","HelloID") },  
        @{ Category = "Virtualization"; Items = @("Microsoft Azure","Hyper-V","Proxmox") },
        @{ Category = "BackupAndRecovery"; Items = @("Azure Recovery Services","Veeam Backup & Replication")},
        @{ Category = "OperatingSystems"; Items = @("Microsoft Windows (Server)","Debian") },
        @{ Category = "Databases"; Items = @("Microsoft SQL Server","Azure SQL","CosmosDB") },
        @{ Category = "ProgrammingAndScripting"; Items = @("PowerShell","Python","T-SQL") },
        @{ Category = "InfrastructureAsCode"; Items = @("Terraform","Ansible") },
        @{ Category = "WorkflowAutomation"; Items = @("Azure Automation","Azure Logic Apps","Power Automate") },
        @{ Category = "Tooling"; Items = @("Azure DevOps","GitHub","Docker","VSCode","Git") }
    )

    IndustryCertifications = @(
        "Microsoft Certified: DevOps Engineer Expert",
        "Microsoft Certified: Azure Solutions Architect Expert",
        "Microsoft Certified: Azure Virtual Desktop Specialty",
        "Microsoft Certified: Azure Cosmos DB Developer Specialty",
        "Microsoft Certified: Azure Database Administrator Associate",
        "Microsoft Certified: Azure Network Engineer Associate",
        "Microsoft Certified: Azure Security Engineer Associate",
        "Microsoft Certified: Azure Administrator Associate",
        "Microsoft Certified: Windows Server Hybrid Administrator Associate",
        "Microsoft Certified: Azure AI Fundamentals",
        "Microsoft Certified: Azure Data Fundamentals",
        "Microsoft Certified: Azure Fundamentals",
        "HelloID Provisioning Associate"
        "HashiCorp Certified: Terraform Associate (expired: june 2025)",
        "AWS Certified Cloud Practitioner (expired: june 2024)"
        "ITIL 4 Foundation"
    )

    RolesInterestedIn = @(
        "Cloud Engineer",
        "Data Platform Engineer",
        "Systems Engineer",
    )
})
```
