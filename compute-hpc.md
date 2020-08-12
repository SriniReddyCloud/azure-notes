# High Performance Computing (HPC) / Big Compute
- HPC uses a large number of CPU or GPU-based computers to solve complex mathematical tasks
- ![image](https://user-images.githubusercontent.com/28542935/89816890-4e240100-db15-11ea-91c8-2ec0c2f02ee4.png)
- Dynamic scaling
- https://docs.microsoft.com/en-us/azure/architecture/topics/high-performance-computing




# Azure Batch
- to run large-scale parallel and high-performance computing (HPC) batch jobs
- creates and manages a pool of compute nodes (virtual machines), installs the applications you want to run, and schedules jobs to run on the nodes
- There is no additional charge for using Batch. You only pay for the underlying resources consumed
- Use cases
  - Intrinsically parallel workloads
    - applications can run independently, and each instance completes part of the work
    - When the applications are executing, they might access some common data, but they do not communicate with other instances of the application
    - Examples:
      - Financial risk modeling using Monte Carlo simulations
      - VFX and 3D image rendering
      - Image analysis and processing
      - Media transcoding
      - Genetic sequence analysis
      - Optical character recognition (OCR)
      - Data ingestion, processing, and ETL operations
      - Software test execution
  - Tightly coupled workloads
    - these are workloads where the applications you run need to communicate with each other, as opposed to run independently. 
    - Tightly coupled applications normally use the Message Passing Interface (MPI) API.
    - Examples
      - Finite element analysis
      - Fluid dynamics
      - Multi-node AI training
  - Large-scale rendering workloads
  - Execution of R algorithms 
- ![image](https://user-images.githubusercontent.com/28542935/89816896-50865b00-db15-11ea-8e85-23b264c2f491.png)


