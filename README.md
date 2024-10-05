%% ER Diagram for Wildfire Management System
erDiagram
USER {
string User_ID PK
string Username
string Password
string Email
string Role
}

    FIRE_EVENT {
      string Fire_ID PK
      string Location
      float Size
      float Temperature
      float Humidity
      string WindDirection
      datetime StartTime
      datetime EndTime
      string Status
    }


    REPORT {
      string Report_ID PK
      string Fire_ID FK
      string User_ID FK
      datetime DateCreated
      string ReportDetails
    }

    RESOURCE {
      string Resource_ID PK
      string ResourceType
      int Quantity
    }

    FIREFIGHTER_ASSIGNMENT {
      string Assignment_ID PK
      string Fire_ID FK
      string User_ID FK
      string Resource_ID FK
      datetime AssignmentTime
      datetime CompletionTime
    }

    ALERT {
      string Alert_ID PK
      string Fire_ID FK
      string Message
      datetime AlertTime
    }

    RISK_ASSESSMENT {
      string Risk_ID PK
      string Location
      string RiskLevel
      datetime AssessmentTime
    }

    AGENCY_DATA {
      string AgencyData_ID PK
      string AgencyName
      string Fire_ID FK
    }

    SENSOR_DATA {
      string SensorData_ID PK
      string Fire_ID FK
      string Satellite_ID
      float Temperature
      string Location
    }


    USER ||--o{ REPORT : "creates"
    USER ||--o{ FIREFIGHTER_ASSIGNMENT : "assigned to"
    FIRE_EVENT ||--o{ SENSOR_DATA : "has"
    FIRE_EVENT ||--o{ REPORT : "reported in"
    FIRE_EVENT ||--o{ FIREFIGHTER_ASSIGNMENT : "involves"
    FIRE_EVENT ||--o{ ALERT : "triggers"
    FIRE_EVENT ||--o{ RISK_ASSESSMENT : "assessed by"
    FIRE_EVENT ||--o{ AGENCY_DATA : "linked with"
    FIREFIGHTER_ASSIGNMENT ||--o{ RESOURCE : "uses"




graph TD
Firefighter -- "Manage Resources" --> System
Firefighter -- "Create Report" --> System
ForestDepartment -- "Assess Risk" --> System
Researcher -- "Access Historical Data" --> System
Public -- "Receive Warnings" --> System

System -- "Notify" --> Firefighter
System -- "Send Alerts" --> Public
System -- "Exchange Data" --> ForestDepartment
System -- "Track Wildfire" --> System
System -- "Generate Reports" --> System
System -- "Detect Wildfire" --> SatelliteSensor
