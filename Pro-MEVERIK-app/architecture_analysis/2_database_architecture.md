# Database Architecture Design for WHC-LiDAR-App

## PostgreSQL Schema  
The database will consist of several interconnected tables. The main entities are as follows:

### Entity - Users  
- **user_id** (Primary Key)  
- username  
- email  
- password_hash  
- created_at  

### Entity - Projects  
- **project_id** (Primary Key)  
- user_id (Foreign Key)  
- project_name  
- description  
- created_at  

### Entity - LIDAR_Scans  
- **scan_id** (Primary Key)  
- project_id (Foreign Key)  
- scan_data (JSONB)  
- timestamp  

### Entity - Settings  
- **setting_id** (Primary Key)  
- user_id (Foreign Key)  
- preferences (JSONB)  

### Entity Relationships  
- A User can have multiple Projects.  
- Each Project can have multiple LIDAR Scans.  
- A User can have multiple Settings entries.  

## Storage Tiers  
1. **Hot Storage**: For active scans and current projects.  
2. **Cold Storage**: For historical scans and archived data that are less frequently accessed.  
3. **Backups**: Regular nightly backups stored offsite.

## Indexing Strategy  
- Index on `user_id` in Projects and Settings for quick user lookups.  
- Index on `project_id` in LIDAR_Scans for fast retrieval of scan data associated with a project.  
- Consider using GIN indexes on JSONB columns for efficient querying.

## Backup Strategy  
- Daily automated backups using `pg_dump` for the entire database.  
- Weekly incremental backups utilizing WAL (Write Ahead Log) archiving to ensure point-in-time recovery.
  
## Scalability Path  
- Initially, a single PostgreSQL instance can handle expected workloads.  
- As usage grows, implement horizontal scaling using read replicas for read-heavy workloads.  
- When necessary, partition tables to improve write performance and manage large datasets carefully.

## Conclusion  
This database architecture is designed to support the scalability needs of the WHC-LiDAR-App while ensuring data integrity and accessibility for users. Each aspect of this architecture has been crafted to align with the operational requirements of the application and future scalability expectations.