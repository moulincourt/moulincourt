```powershell
class Engineer {
    [string]    $Name
    [string]    $Gender
    [string[]]  $Pronouns
    [string]    $Country
    [string]    $Province
    [string]    $City
    [string]    $AlmaMater
    [string]    $DiscStyle
    [string]    $MbtiType
    [string[]]  $Traits
    [string[]]  $Interests
    [hashtable] $Socials
    [hashtable] $HasExperienceWith
    [string[]]  $Certifications
    [string[]]  $RolesInterestedIn

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
$Team += [Engineer]::new(@{
    Name      = "Wouter van den Meulenhof"
    Gender    = "Male"
    Pronouns  = @("He", "Him", "His")
    Country   = "The Netherlands"
    Province  = "North Brabant"
    City      = "Helmond"
    AlmaMater = "Fontys University of Applied Sciences"
    DiscStyle = "C"
    MbtiType  = "INTJ"
    Traits    = @("Informal", "Curious", "Enthusiastic")
    Interests = @("Computers", "History", "Sci-fi", "Board Games", "LEGO")

    Socials = @{
        LinkedIn = "https://www.linkedin.com/in/moulincourt"
        Credly   = "https://www.credly.com/users/moulincourt"
        GitHub   = "https://github.com/moulincourt"
    } 

    HasExperienceWith = @{
        WaysOfWorking    = @( "Agile/Scrum", "ITIL", "GitOps", "DevOps" )
        Identity         = @( "Microsoft Entra", "Active Directory", "FreeIPA", "HelloID")
        CloudProviders   = @( "Microsoft Azure" )
        Virtualization   = @( "Hyper-V", "Proxmox" )
        Backup           = @( "Azure Recovery Services", "Veeam Backup & Replication" )
        OperatingSystems = @( "Windows Server", "Debian", "Ubuntu", "Fedora" )
        Databases        = @( "Microsoft SQL Server", "PostgreSQL", "Azure SQL", "Azure Cosmos DB" )
        Automation       = @( "Azure Automation", "Azure Logic/Function/Container Apps", "n8n" )
        Coding           = @( "OpenTofu", "Ansible", "PowerShell", "Python" "T-SQL", "Bash" )
        Tools            = @( "Azure DevOps", "GitHub", "Docker", "VS Code", "Git" )
    }

    Certifications = @(
        "Microsoft Certified: DevOps Engineer Expert",
        "Microsoft Certified: Azure Solutions Architect Expert",
        "Microsoft Certified: Azure for SAP Workloads Specialty",
        "Microsoft Certified: Azure Virtual Desktop Specialty",
        "Microsoft Certified: Azure Cosmos DB Developer Specialty",
        "Microsoft Certified: Azure Database Administrator Associate",
        "Microsoft Certified: Azure Network Engineer Associate",
        "Microsoft Certified: Azure Security Engineer Associate",
        "Microsoft Certified: Azure Administrator Associate",
        "Microsoft Certified: Windows Server Hybrid Administrator Associate",
        "Microsoft Certified: Identity and Access Administrator Associate",
        "Microsoft Certified: Security, Compliance, and Identity Fundamentals",
        "Microsoft Certified: Azure AI Fundamentals",
        "Microsoft Certified: Azure Data Fundamentals",
        "Microsoft Certified: Azure Fundamentals",
        "HashiCorp Certified: Terraform Associate (expired: June 2025)",
        "AWS Certified: Cloud Practitioner (expired: June 2024)",
        "HelloID Provisioning Associate",
        "HelloID Provisioning Fundamentals",
        "ITIL 4 Foundation"
    )

    RolesInterestedIn = @(
        "Systems Engineer",
        "Database Reliability Engineer",
        "Cloud Engineer",
        "Technical Application Manager"
    )
})
```
