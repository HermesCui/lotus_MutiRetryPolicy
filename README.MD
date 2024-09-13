**Xinjing Zhou**, Xiangyao Yu, Goetz Graefe, Micheal Stonebraker

[Lotus: Scalable Multi-Partition Transactions on Single-Threaded Partitioned Databases](https://doi.org/10.14778/3551793.3551843)

*Proc. of the VLDB Endowment (PVLDB), Volume 15, Sydney, Australia, 2022.*

This repository contains source code for Lotus. The code is based on the [star](https://github.com/luyi0619/star) framework from Yi Lu.

# Dependencies

```sh
sudo apt-get update
sudo apt-get install -y zip make cmake g++ libjemalloc-dev libboost-dev libgoogle-glog-dev
```

# Build

```
mkdir -p build
cd build
cmake ..
make -j
```

# Example commands to run the project in a single host

```
# TPCC
./build/bench_tpcc --logtostderr=1 --id=0 --servers="127.0.0.1:1234" --threads=2 --partition_num=2 --granule_count=2000 \
        --log_path= --persist_latency=0 --wal_group_commit_time=0 --wal_group_commit_size=0 \
        --partitioner=hash --hstore_command_logging=false \
        --replica_group=1 --lock_manager=0 --batch_flush=1 --lotus_async_repl=true --batch_size=0 \
        --protocol=Sundial --query=mixed --neworder_dist=10 --payment_dist=15

./build/bench_tpcc --logtostderr=1 --id=0 --servers="127.0.0.1:1234" --threads=2 --partition_num=2 --granule_count=2000 \
        --log_path= --persist_latency=0 --wal_group_commit_time=0 --wal_group_commit_size=0 \
        --partitioner=hash --hstore_command_logging=false \
        --replica_group=1 --lock_manager=0 --batch_flush=1 --lotus_async_repl=true --batch_size=0 \
        --protocol=HStore --query=mixed --neworder_dist=10 --payment_dist=15

# YCSB
./build/bench_ycsb --logtostderr=1 --id=0 --servers="127.0.0.1:1234" --threads=2 --partition_num=2 --granule_count=2000 \
        --log_path= --persist_latency=0 --wal_group_commit_time=0 --wal_group_commit_size=0 \
        --partitioner=hash --hstore_command_logging=false \
        --replica_group=1 --lock_manager=0 --batch_flush=1 --lotus_async_repl=true --batch_size=0 \
        --protocol=Sundial --keys=100000 --read_write_ratio=100 --zipf=0 --cross_ratio=10 --cross_part_num=2

./build/bench_ycsb --logtostderr=1 --id=0 --servers="127.0.0.1:1234" --threads=2 --partition_num=2 --granule_count=2000 \
        --log_path= --persist_latency=0 --wal_group_commit_time=0 --wal_group_commit_size=0 \
        --partitioner=hash --hstore_command_logging=false \
        --replica_group=1 --lock_manager=0 --batch_flush=1 --lotus_async_repl=true --batch_size=0 \
        --protocol=HStore --keys=100000 --read_write_ratio=100 --zipf=0 --cross_ratio=10 --cross_part_num=2
```