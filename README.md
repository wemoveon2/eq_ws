# README

Data engineering work samples for EQ Works. Utilizes Apache Spark and Apache Airflow. 

Solutions for the common questions can be found [here](https://github.com/wemoveon2/data_eng_work_sample/blob/main/common_problems.ipynb).
The DAG file for Airflow can be found [here](https://github.com/wemoveon2/data_eng_work_sample/blob/main/dag_candidate_final.py).

## Common Problems

The notebook removes **all** records with **identical** `geoinfo` and `timest` from `~/data/DataSample.csv`. Records with `timest` differences in the range of miliseconds are not considered as identical even with identical `geoinfo`. 

Final DataFrame containing the non-suspicious records and the assigned `POIID` based on shortest haversine distance in kilometers is written out to `~/data/DataSample_Assigned.csv`.

## Data Track Problems

The DAG file requires the `postgres` connection at port 5432 as seen [here](https://github.com/wemoveon2/data_eng_work_sample/blob/main/ws-data-pipeline/docker-compose.yml). 

- DAG Config
	- [x] Scheduled to run every minute.
	- [x] Pipeline automatically scheduled to run without manual triggering when placed in `./dag` folder.
	- [x] No backfilling.
	- [x] No retrying if one run fails.
	- [x] Scheduled to run even if previous fails (don't set `depends_on_past=True` for tasks).
- Pipeline Tasks
	- [x] 1. Create tables if they don't exist.
	- [x] 2. Insert new records into tables.
	- [x] 3. Generate given number of digits from 0 to 9 and get count within string.
	- [x] 4. Runs only if task 3 fails, updates records created by task 2, ends pipeline.
	- [x] 5. Runs if 3 successful, branches depending on if value from task 3 is G/L than threshold.
	- [x] 6. Update records created by 2 to indicate count is greater, ends pipeline.
	- [x] 7. Updates records created by 2 to indicate count is lesser, ends pipeline.