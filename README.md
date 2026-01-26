```PowerShell
$Team += [Engineer]::new(@{
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
        @{ Name = "GitHub";   Url = "https://github.com/moulincourt" } 
    )

    HasExperienceWith = @(
        @{ Category = "WaysOfWorking"; Items = @("Agile/Scrum","ITIL","GitOps","DevOps") }
        @{ Category = "IdentityAndAccess"; Items = @("Microsoft Entra","Active Directory","HelloID") }
        @{ Category = "CloudAndVirtualization"; Items = @("Microsoft Azure","Hyper-V","Proxmox") }
        @{ Category = "BackupAndReplication"; Items = @("Azure Recovery Services","Veeam Backup & Replication") }
        @{ Category = "OperatingSystems"; Items = @("Microsoft Windows Server","Debian","Ubuntu") }
        @{ Category = "Databases"; Items = @("Microsoft SQL Server","Azure SQL","Azure Cosmos DB","Azure Tables") }
        @{ Category = "ProgrammingAndScripting"; Items = @("PowerShell","Python","T-SQL","Bash") }
        @{ Category = "InfrastructureAsCode"; Items = @("OpenTofu","Terraform","Ansible") }
        @{ Category = "Automation"; Items = @("Azure Automation","Azure Logic Apps","Azure Functions","Azure Container Apps")}
        @{ Category = "Tooling"; Items = @("Azure DevOps","GitHub","Docker","Git","VS Code") }
    )

    IndustryCertifications = @(
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
        "HelloID Provisioning Associate",
        "HashiCorp Certified: Terraform Associate (expired: June 2025)",
        "ITIL 4 Foundation"
    )

    RolesInterestedIn = @(
        "Cloud Engineer",
        "Systems Engineer",
        "Technical Application Manager"
    )
})

```
