---
layout: page
permalink: /blogs/index.html
title: Blogs
---

 > Posted on 2024-04-16

###  Project Members:

  - Xuanye Chen
  - Zhenzhe Li
  - Ruijie Jian
  - Huasen Xi

### Project Summary:

  As part of our final project, we aim to integrate an efficient Multigrid-preconditioned Conjugate Gradient (MGPCG) method into our GPU-based fluid simulation system. This algorithm is crucial for solving the projection Poisson equation efficiently, which is a central component of maintaining the incompressibility of the fluid in our simulation.

####  Current Progress:

  1. **Initial Research and Planning (Completed)**

     - **Date:** Week 1 of Project Timeline
     - Activities:
       - Conducted a comprehensive review of the literature on MGPCG algorithms and their application in fluid dynamics.
       - Defined the algorithm's role within the context of our fluid simulation framework.
     - Outcome:
       - Established a clear understanding of the algorithm's mathematical foundation and its relevance to our project goals.
       - Developed an initial algorithmic flowchart and integration strategy with the fluid simulation pipeline.

  2. **Development of MGPCG Algorithm Prototype (In Progress)**

     - **Date:** Week 2 of Project Timeline

     - Activities:

       - Started coding the basic structure of the MGPCG algorithm in Python for conceptual testing.
       - Integrated simple test cases to validate the correctness of the prototype.

     - Current Status:

       - We have successfully implemented the grid discretization for the Poisson equation and developed functions for coarsening the grid as part of our approach to solve the equation. Additionally, several sub-functions including iterative processes and smoothers have been completed. However, we are still encountering issues with solving the overall equation programmatically, which is our current focus to resolve.

       <br>

       <div>
       <img src="/images/grid.png">
       </div>


       after downsample:
    
       <br>
    
       <div>
       <img src="/images/downsample_grid.png">
       </div>
    
     - Challenges Encountered:
    
       - Despite the progress in developing the necessary components of the MGPCG algorithm, there are still reservations about the efficiency and stability of the convergence of the algorithm. Ensuring the high performance and reliable convergence of the algorithm remains a significant challenge, which we are actively working to address. We anticipate resolving these issues shortly, but the concerns about algorithmic efficiency and stability are ongoing.

  3. **Wavefront Path Tracing Renderer Development (In Progress)**

     - **Date:** Concurrent with MGPCG development
     - Activities:
       - Implemented wavefront path tracing based on the "Megakernels Considered Harmful: Wavefront Path Tracing on GPUs" by Vinkler et al., and optimized the ray-scene intersection computation.
       - Integrated Multiple Importance Sampling (MIS) to combine light sampling and BSDF sampling efficiently.
     - Current Status:
       - The renderer has been tested on the CBbunny scene, outperforming a CPU multi-threaded path tracer by completing the task in half the time. The use of MIS has significantly sped up convergence:
       
       <br>
     
       <div>
       <img src="/images/bunny.png">
       </div>
     - Challenges Encountered:
       - The images produced by the wavefront path tracer are dimmer than those produced by the CPU path tracer. Investigating the causes for this issue and exploring the integration of volumetric rendering within the wavefront path tracing framework.
  
  4. **Development of GPU-Accelerated Multigrid Poisson Solver (In Progress)**
  
     - **Date:** Concurrent with MGPCG development
   - Current Status:
     
       - We have implemented a multigrid solver for the 2D Poisson equation with Dirichlet boundary conditions, utilizing second-order finite differences for discretization and conservative prolongation and restriction operators.
       - The solver has two versions: one that runs on a single-threaded CPU and another optimized for GPU using custom CUDA kernels. The GPU solver employs a Red-Black Gauss-Seidel smoother to exploit parallelism effectively.
     - Performance tests show that the CUDA-based solver drastically reduces the number of iterations needed to achieve low residuals, proving its efficiency over the CPU-based approach in terms of both speed and accuracy.
     - Challenges Encountered:
     - The current GPU solver implementation heavily mirrors the structure of the CPU solver, leading to significant code duplication and potential inefficiencies.
       - Initial profiling indicates several optimization opportunities. Particularly, the current Red-Black Gauss-Seidel implementation is suboptimal, requiring multiple DRAM trips to load data for red and black points separately, which only activates half of the GPU threads at a time.
       - Plans are underway to refactor this implementation to utilize shared memory more effectively, allowing for concurrent activation of all threads and reducing memory traffic. Combining some kernels, such as the restriction and residual kernels, into a single operation could further optimize performance.

  5. **Performance Evaluation and Final Adjustments (Upcoming)**
  
     - **Planned Start Date:** Week 4 of Project Timeline
     - Planned Activities:
       - Benchmark the performance of the GPU-based systems against the existing CPU-based systems.
     - Address any identified performance bottlenecks.
       - Finalize integration and prepare for the project demonstration.
   - Goals:
       - Achieve significant performance improvements over the CPU-based systems.
       - Ensure the physical correctness of the simulation and rendering results.

#### Next Steps:

- Complete the GPU porting of the MGPCG algorithm and the wavefront path tracing framework.
  - Begin comprehensive integration testing with the complete simulation and rendering system.
- Conduct detailed performance analysis to identify and address any inefficiencies.
  

