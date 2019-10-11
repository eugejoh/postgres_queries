# Useful Postgres SQL Commands and Queries
Eugene Joh

This repository contains Postgres SQL queries that are commonly used and acts as a cheatsheet for useful SQL queries.



# Get Field Types ---------------------------------------------------------
SELECT attname, format_type(atttypid, atttypmod) AS type
FROM   pg_attribute
WHERE  attrelid = 'child_copy'::regclass
AND    attnum > 0
AND    NOT attisdropped
ORDER  BY attnum;


# Get Field Comments ------------------------------------------------------
SELECT c.table_schema,c.table_name,c.column_name,pgd.description
FROM pg_catalog.pg_statio_all_tables as st
inner join pg_catalog.pg_description pgd on (pgd.objoid=st.relid)
inner join information_schema.columns c on (pgd.objsubid=c.ordinal_position
                                            and  c.table_schema=st.schemaname and c.table_name=st.relname)
WHERE table_name = 'srs_rd3_hh';


# Get Table Comment -------------------------------------------------------
SELECT relname, obj_description(oid)
FROM pg_class
WHERE relkind = 'r'
AND relname = 'srs_rd3_hh';

