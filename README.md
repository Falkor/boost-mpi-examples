# Boost MPI examples
This repo follows the tutorial of the [official site](http://www.boost.org/doc/libs/1_65_1/doc/html/mpi/tutorial.html). The official site doesn't provide the deployable source; thus this is what I am doing here.

_Note_: if you use boost version over 1.66, you **need** to rely on CMake 3.11.x or above -- see [description on the Pull request #6724](https://github.com/easybuilders/easybuild-easyconfigs/pull/6724).

## Build  (using foss toolchain)

```bash
# Eventually
$> module load devel/Boost/1.66.0-foss-2018a
$> module load devel/CMake/3.12.1-GCCcore-6.4.0

$> mkdir build.foss
$> cd build.foss
$> cmake ../src
$> make -j $SLURM_NTASKS_PER_NODE

# Typical run on slurm-based cluster
$> for f in example*; do echo "==> $f"; srun -n $SLURM_NTASKS $f; done
```

## Build (using Intel toolchain)

For instance on a Slurm-based HPC system:

```bash
# Eventually
$> module load devel/Boost/1.66.0-intel-2018a
$> module load devel/CMake/3.12.1-intel-2018a


$> mkdir build.intel
$> cd build.intel
$> CXX=icpc cmake ../src
$> make -j $SLURM_NTASKS_PER_NODE

# Typical run on slurm-based cluster
$> for f in example*; do echo "==> $f"; srun -n $SLURM_NTASKS $f; done
```

## Run

For example, to run `example1-setup` with 4 processes:

```
mpirun -np 4 example1-setup
```

On a Slurm-based cluster:

```
srun -n $SLURM_NTASKS ./example<>...
```
