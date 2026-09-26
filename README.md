# Performance Analysis of Matrix Multiplication

## 🔬 Parallel & GPU Computing Laboratory

| **Course** | **Workload** | **Computing Models** | **Status** |
|---|---|---|---|
| Parallel & GPU Computing | 4000 × 4000 Matrix Multiplication | Sequential • OpenMP • MPI • CUDA | ✅ Completed |

---

## 📌 Project Overview

This project implements and analyzes **4000 × 4000 matrix multiplication** using four different computing approaches:

- 🖥️ Sequential CPU
- ⚡ OpenMP Shared Memory
- 🌐 MPI Distributed Memory
- 🚀 CUDA GPU Computing

The objective is to implement the same matrix multiplication problem using different computing models and compare their execution time and speedup.

---

## 🎯 Objectives

The main objectives of this experiment are:

1. Implement matrix multiplication using sequential CPU execution.
2. Implement matrix multiplication using OpenMP.
3. Implement distributed matrix multiplication using MPI.
4. Implement matrix multiplication using CUDA.
5. Measure the execution time of each implementation.
6. Calculate the speedup of the parallel implementations.
7. Verify the correctness of the results.
8. Compare different parallel computing architectures.

---

## 🧮 Problem Description

The experiment performs matrix multiplication:

```text
C = A × B
```

The matrices used are:

```text
A = 4000 × 4000
B = 4000 × 4000
C = 4000 × 4000
```

Every element of matrices `A` and `B` is initialized to `1.0`.

The matrix multiplication is performed using:

```text
C[i][j] = Σ A[i][k] × B[k][j]
```

Since every element is `1.0`, the expected result is:

```text
C[0][0] = 4000.00
```

This value is used to verify the correctness of all four implementations.

---

## ⚙️ Computing Models

### 1. Sequential CPU

The sequential implementation performs matrix multiplication using traditional nested loops.

The computation is executed sequentially on the CPU and is used as the baseline for performance comparison.

**Characteristics:**

- Single-threaded execution
- CPU-based computation
- Traditional nested-loop implementation
- Used as the baseline

---

### 2. OpenMP

OpenMP is used to parallelize the matrix multiplication across multiple CPU threads.

The experiment uses:

```text
8 CPU Threads
```

OpenMP follows a shared-memory programming model where multiple threads access the same memory space.

**Characteristics:**

- Shared-memory parallelism
- Multiple CPU threads
- Parallel loop execution
- 8 threads used

---

### 3. MPI

MPI is used to distribute the matrix multiplication across multiple processes.

The experiment uses:

```text
4 MPI Processes
```

The computation is distributed across Ubuntu virtual machines.

The MPI implementation uses:

```text
MPI_Scatter
MPI_Bcast
MPI_Gather
```

**Characteristics:**

- Distributed-memory computing
- 4 MPI processes
- Multiple Ubuntu virtual machines
- Process-to-process communication

---

### 4. CUDA

CUDA is used to perform matrix multiplication on a GPU.

The CUDA implementation uses a two-dimensional grid of blocks and threads.

**CUDA Configuration:**

```text
Matrix Size       : 4000 × 4000
Block Size        : 16 × 16
Grid Size         : 250 × 250
Total Blocks      : 62,500
Threads per Block : 256
```

---

## 📊 Workload Specification

| Parameter | Value |
|---|---|
| Matrix A | 4000 × 4000 |
| Matrix B | 4000 × 4000 |
| Matrix C | 4000 × 4000 |
| Elements of A | 1.0 |
| Elements of B | 1.0 |
| Operation | C = A × B |
| Expected C[0][0] | 4000.00 |

### Correctness Verification

All four implementations are expected to produce:

```text
C[0][0] = 4000.00
```

---

## 📁 Repository Structure

```text
PGC-LAB/
│
├── images/
│   ├── sequential_result.png
│   ├── openmp_result.png
│   ├── openmp_htop.png
│   ├── mpi_ping.png
│   ├── mpi_send_recv.png
│   ├── mpi_result.png
│   ├── cuda_result.png
│   ├── performance_comparison_charts.png
│   ├── execution_time_chart.png
│   └── speedup_chart.png
│
├── scripts/
│
├── src/
│   ├── sequential/
│   │   └── matrix_sequential.c
│   │
│   ├── openmp/
│   │   └── matrix_openmp.c
│   │
│   ├── mpi/
│   │   ├── matrix_mpi.c
│   │   └── mpi_send_recv.c
│   │
│   └── cuda/
│       └── matrix_cuda.cu
│
├── README.md
└── LICENSE
```

---

## 💻 Source Code

### Sequential

```text
src/sequential/matrix_sequential.c
```

Sequential CPU implementation of matrix multiplication.

### OpenMP

```text
src/openmp/matrix_openmp.c
```

OpenMP-based shared-memory implementation.

### MPI

```text
src/mpi/matrix_mpi.c
```

MPI-based distributed matrix multiplication.

MPI communication test:

```text
src/mpi/mpi_send_recv.c
```

### CUDA

```text
src/cuda/matrix_cuda.cu
```

CUDA GPU implementation of matrix multiplication.

---

# 🚀 Compilation and Execution

## Sequential CPU

Navigate to the sequential directory:

```bash
cd src/sequential
```

Compile:

```bash
gcc -O2 matrix_sequential.c -o matrix_sequential
```

Run:

```bash
./matrix_sequential
```

Expected output verification:

```text
C[0][0] = 4000.00
```

---

## OpenMP

Navigate to the OpenMP directory:

```bash
cd src/openmp
```

Compile:

```bash
gcc -O2 -fopenmp matrix_openmp.c -o matrix_openmp
```

Set the number of threads:

```bash
export OMP_NUM_THREADS=8
```

Run:

```bash
./matrix_openmp
```

Expected output verification:

```text
C[0][0] = 4000.00
```

---

## MPI

Navigate to the MPI directory:

```bash
cd src/mpi
```

Compile:

```bash
mpicc -O2 matrix_mpi.c -o matrix_mpi
```

Run using four processes:

```bash
mpirun -np 4 --hostfile hosts sh -c '$HOME/matrix_mpi'
```

Expected output verification:

```text
C[0][0] = 4000.00
```

---

## CUDA

Navigate to the CUDA directory:

```bash
cd src/cuda
```

Compile:

```bash
nvcc -O2 matrix_cuda.cu -o matrix_cuda
```

Run:

```bash
./matrix_cuda
```

Expected output verification:

```text
C[0][0] = 4000.00
```

---

# 📈 Experimental Results

All four implementations produced the expected verification value:

```text
C[0][0] = 4000.00
```

## Sequential CPU

**Execution Time:**

```text
244.120000 seconds
```

**Verification:**

```text
C[0][0] = 4000.00
```

![Sequential Result](images/sequential_result.png)

---

## OpenMP

**Number of Threads:**

```text
8
```

**Execution Time:**

```text
30.830434 seconds
```

**Verification:**

```text
C[0][0] = 4000.00
```

![OpenMP Result](images/openmp_result.png)

### OpenMP CPU Monitoring

![OpenMP htop](images/openmp_htop.png)

---

## MPI

**Number of Processes:**

```text
4
```

**Execution Time:**

```text
92.979510 seconds
```

**Verification:**

```text
C[0][0] = 4000.00
```

![MPI Result](images/mpi_result.png)

### MPI Network Verification

![MPI Ping](images/mpi_ping.png)

### MPI Communication Test

![MPI Send Receive](images/mpi_send_recv.png)

---

## CUDA

**Kernel Execution Time:**

```text
0.146443 seconds
```

**Total CUDA Phase:**

```text
0.165004 seconds
```

**Verification:**

```text
C[0][0] = 4000.00
```

![CUDA Result](images/cuda_result.png)

---

# 📊 Performance Comparison

| Computing Model | Architecture | Resources | Execution Time | Speedup | Verification |
|---|---|---|---:|---:|---:|
| Sequential | CPU | 1 Thread | 244.120000 s | 1.00× | 4000.00 |
| OpenMP | Shared Memory | 8 Threads | 30.830434 s | 7.92× | 4000.00 |
| MPI | Distributed Memory | 4 Processes | 92.979510 s | 2.63× | 4000.00 |
| CUDA | GPU | GPU Threads | 0.165004 s | 1479.48× | 4000.00 |

---

## 📉 Performance Graphs

### Overall Performance Comparison

![Performance Comparison](images/performance_comparison_charts.png)

### Execution Time

![Execution Time](images/execution_time_chart.png)

### Speedup

![Speedup](images/speedup_chart.png)

---

# 🔍 Performance Analysis

## Sequential

The sequential implementation required:

```text
244.120000 seconds
```

This execution time is used as the baseline for calculating speedup.

---

## OpenMP

The OpenMP implementation used 8 CPU threads.

Execution time:

```text
30.830434 seconds
```

Measured speedup:

```text
7.92×
```

OpenMP improves the execution time by distributing the computation among multiple CPU threads.

---

## MPI

The MPI implementation used 4 processes.

Execution time:

```text
92.979510 seconds
```

Measured speedup:

```text
2.63×
```

The workload is distributed among multiple processes. Communication between distributed processes contributes to the total execution time.

---

## CUDA

The CUDA implementation recorded:

```text
Kernel Execution Time = 0.146443 seconds
Total CUDA Phase      = 0.165004 seconds
```

Measured speedup using the total CUDA phase:

```text
1479.48×
```

The CUDA implementation uses GPU parallelism to execute a large number of matrix multiplication operations simultaneously.

---

# 📷 Screenshots

The `images` directory contains screenshots and performance graphs from the experiment.

### Sequential

- Source code
- Compilation
- Execution
- Final output

### OpenMP

- Source code
- Thread configuration
- Execution
- CPU monitoring
- Final output

### MPI

- VM connectivity
- Ping verification
- MPI communication
- MPI execution
- Final output

### CUDA

- GPU verification
- CUDA compiler verification
- Compilation
- GPU execution
- Final output

---

# 🏁 Conclusion

This laboratory experiment implemented and compared four different approaches for matrix multiplication:

```text
Sequential
OpenMP
MPI
CUDA
```

A `4000 × 4000` matrix multiplication workload was used for all implementations.

All four implementations produced the expected result:

```text
C[0][0] = 4000.00
```

The measured execution times were:

| Implementation | Execution Time |
|---|---:|
| Sequential | 244.120000 s |
| OpenMP | 30.830434 s |
| MPI | 92.979510 s |
| CUDA | 0.165004 s |

The measured speedups were:

| Implementation | Speedup |
|---|---:|
| Sequential | 1.00× |
| OpenMP | 7.92× |
| MPI | 2.63× |
| CUDA | 1479.48× |

The experiment demonstrates the differences between sequential execution, shared-memory parallelism, distributed-memory parallelism, and GPU-based parallel computing.

---

# 🛠️ Technologies Used

- C
- OpenMP
- MPI
- CUDA
- GCC
- NVIDIA CUDA Toolkit
- Ubuntu
- Git
- GitHub

---

# 👩‍💻 Author

**Anushree Angadi**

GitHub Repository:

[PGC-LAB](https://github.com/anushree-angadi/PGC-LAB)

---

## 📚 Academic Project

This project was completed as part of the **Parallel & GPU Computing Laboratory**.

The experiment focuses on implementing, executing, measuring, and comparing different approaches to parallel matrix multiplication.
