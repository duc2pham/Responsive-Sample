# home_responsive_sample

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

graph TD
    %% Define Layers
    subgraph Presentation Layer
        direction TB
        P_Widgets[Flutter Widgets] --> P_Bloc[Bloc / ViewModel]
    end

    subgraph Domain Layer
        direction TB
        D_UseCase(LoginUseCase) --> D_RepoInterface(AuthenticateRepository Interface)
        D_UseCase -- uses --> D_Entity(UserEntity)
    end

    subgraph Data Layer
        direction TB
        Data_RepoImpl(Repository Implementation) --> Data_DataSource[DataSource (API/DB)]
        Data_DataSource -- uses --> Data_RequestModel(UserRequest Model)
        Data_DataSource -- returns --> Data_ResponseModel(UserResponse Model)
        Data_RepoImpl -- uses --> Data_RequestModel
        Data_RepoImpl -- maps to/from --> Data_ResponseModel
        Data_RepoImpl -- maps to --> D_Entity
    end

    %% Define Dependencies (Arrows point WITH the dependency)
    P_Bloc --> D_UseCase  // Presentation depends on Domain (UseCase)
    Data_RepoImpl -- implements --> D_RepoInterface // Data implements Domain interface
    Data_RepoImpl --> D_Entity // Data knows about Domain Entities for mapping

    %% Styling (Optional, for clarity)
    style P_Widgets fill:#lightblue,stroke:#333,stroke-width:2px
    style P_Bloc fill:#lightblue,stroke:#333,stroke-width:2px
    style D_UseCase fill:#lightgreen,stroke:#333,stroke-width:2px
    style D_RepoInterface fill:#lightgreen,stroke:#333,stroke-width:2px
    style D_Entity fill:#lightgreen,stroke:#333,stroke-width:2px
    style Data_RepoImpl fill:#lightcoral,stroke:#333,stroke-width:2px
    style Data_DataSource fill:#lightcoral,stroke:#333,stroke-width:2px
    style Data_RequestModel fill:#lightcoral,stroke:#333,stroke-width:2px
    style Data_ResponseModel fill:#lightcoral,stroke:#333,stroke-width:2px

