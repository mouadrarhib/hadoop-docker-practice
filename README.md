
# Hadoop Docker Practice Setup

This repository contains a ready-to-run Docker Compose setup for practicing Apache Hadoop on your local machine.  
It includes a pseudo-distributed Hadoop cluster with:

- **HDFS** (NameNode + DataNode)
- **YARN** (ResourceManager + NodeManager)
- **MapReduce** support
- **HistoryServer** for job tracking

---

## Prerequisites

- Docker Desktop installed (Windows, Mac, or Linux)
- At least 4 GB RAM allocated to Docker
- Basic familiarity with Docker and Hadoop commands

---

## Getting Started

1. Clone this repository:

```bash
git clone https://github.com/your-username/hadoop-docker-practice.git
cd hadoop-docker-practice
```

2. Start the Hadoop cluster:

```bash
docker-compose up -d
```

3. Wait ~30 seconds for all services to initialize.

4. Access the Web UIs:

- NameNode (HDFS): http://localhost:9870
- DataNode: http://localhost:9864
- ResourceManager (YARN): http://localhost:8088
- NodeManager: http://localhost:8042
- HistoryServer: http://localhost:8188

---

## Usage

Enter the NameNode container to run Hadoop commands:

```bash
docker exec -it namenode bash
```

Example Hadoop commands:

- Create a directory in HDFS:
  ```bash
  hdfs dfs -mkdir /test
  ```
- Upload a file to HDFS:
  ```bash
  echo "Hello Hadoop" > file.txt
  hdfs dfs -put file.txt /test
  ```
- List files in HDFS:
  ```bash
  hdfs dfs -ls /test
  ```
- Run a MapReduce example job (wordcount):
  ```bash
  hadoop jar /opt/hadoop-3.2.1/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.2.1.jar wordcount /test /output
  hdfs dfs -cat /output/part-r-00000
  ```

---

## Stopping the Cluster

To stop and remove containers and volumes:

```bash
docker-compose down -v
```

---

## Notes

- This setup is for learning and practice only; not intended for production.
- Volumes are used to persist HDFS data between restarts.
- You can modify `docker-compose.yml` to customize the cluster as needed.

---

## Troubleshooting

- If DataNode does not register, restart the cluster with volumes cleared:

  ```bash
  docker-compose down -v
  docker-compose up -d
  ```

- Ensure Docker has enough RAM allocated (minimum 4 GB).

---

Feel free to open issues or contribute improvements!

---

*Happy Hadoop practicing! 🚀*
