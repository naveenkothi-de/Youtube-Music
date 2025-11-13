YouTube Music Data Pipeline — AWS Glue | Athena | QuickSight

Project Overview

This project demonstrates how to build a serverless data lakehouse architecture on AWS to transform, catalog, and visualize music analytics data. Using AWS Glue, S3, Athena, and QuickSight, raw CSV data is converted into optimized Parquet format and made query-ready for interactive dashboards — without any servers or manual schema management.

S3 Staging --> Gule ETL --> S3 Data Warehouse --> Crawler --> Athena --> QuicKsight

-> Components
Component: Raw Storage AWS Service: Amazon S3 (Staging) Purpose: Stores raw CSV data (artists, albums, tracks).
Component: ETL Processing AWS Service: AWS Glue ETL Job Purpose: Cleans, joins, and converts CSV → Parquet.
Component: Curated Zone AWS Service: Amazon S3 (Data Warehouse) Purpose: Stores transformed, analytics-ready data.
Component: Metadata Catalog AWS Service: AWS Glue Crawler Purpose: Creates tables and schema in Glue Catalog.
Component: Query Engine AWS Service: Amazon Athena Purpose: Runs SQL directly on S3 data.
Component: Visualization AWS Service: Amazon QuickSight Purpose: Builds BI dashboards for insights.

-> Datasets

File: artists.csv Description: Artist ID, name, genre, followers, popularity
File: albums.csv Description: Album ID, artist ID, name, release date
File: tracks.csv Description: Track ID, album ID, duration, popularity

--> Implementation Steps:

Upload Raw Data to S3 (Staging Layer)
Upload CSV files to the following S3 path:
s3://youtube-music22/staging/
Files: 
• s3://youtube-music22/staging/artists.csv
• s3://youtube-music22/staging/albums.csv 
• s3://youtube-music22/staging/tracks.csv

2. Build Glue ETL Job
Data Sources: The 3 CSV files in S3 staging.

Transformations: 
• Select key columns: artist_name, track_name, album_name, genre, release_date 
• Convert data types: date, int, string • Write output as Parquet

Target Path: s3://youtube-music22/warehouse/
1. Run AWS Glue Crawler
2. Data source: s3://youtube-music22/warehouse/
3. Crawler database: youtube_music
4. Output table: warehouse_youtube_music
5. Classification: parquet
6. Role: glue_access with S3 + CloudWatch + PassRole permissions.
   
7. Query with Athena
   
8. Visualize with QuickSight
    * Connect to Athena → choose youtube_music database.
    * Import warehouse_youtube_music table.
    * Create visuals:
    * Top Artists by Followers
    * Songs Released per Year
    * Track Popularity Distribution
    * Publish the dashboard for interactive exploration.
      
Tech Stack
• AWS S3 – Data Lake Storage
 • AWS Glue ETL – Data Processing
• AWS Glue Crawler & Catalog – Metadata Management
 • Amazon Athena – Serverless SQL
 • Amazon QuickSight – Visualization & BI
• Parquet Format – Optimized Storage

Results
• Transformed 3 raw CSVs -> single Parquet dataset.
 • Reduced query cost by 80 % using Parquet compression.
• Achieved end-to-end automation with no servers.
• Delivered live dashboards for music analytics within minutes.
