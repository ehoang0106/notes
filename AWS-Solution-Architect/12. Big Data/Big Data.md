[[Big Data]], [[AWS]], [[Redshift]]

# Big Data overview

What are the 3 Vs of big data?
-Refer to 3 primary characteristics that are often to describe
- **Volume**: Ranges from terabytes to petabytes of data
- **Variety**: Includes data from wide range of sources and formats
- **Velocity**: Data needs to be collected, stored, processed, and analyzed within short period of time

## Redshift
### Overview and uses

- Redshift is a fully managed data warehouse service in the cloud, handles massive amount of data on petabytes scale
- It's a very large relational database traditionally in big data applications

- Size: Redshift is big, can hold up to 16 PB.
- Relational: This is database relational. Can use standard SQL and BI to interact
- Based on PostgreSQL: but it not used for online transaction workloads
- Usage: Redshift is not meant to be replacement for standard RDS
- High performance: 10x performance
- Columnar: Storage is column-based instead of row-based
### Redshift Spectrum

Allows you to directly run SQL queries against exabytes of unstructured data in S3 without needing to load or transform data

### Exam Tips

- Any scenarios needing to optimize Redshift insert performance -> large data inserts, it's mean you should leverage large batch insert whenever you can
- Don't use Redshift to replace RDS
- Redshift is RD based on PostgreSQL
- Support up to 16 PB
- Can deploy a multi-AZ cluster for HA
- Use Redshift spectrum to efficiently and quickly process data in S3
- Leverage snapshots for point-in-time recovery, restoration to other regions