# Drop existing foreign key

```sql
-- Check if the foreign key exists before attempting to drop it
SET @fk_name = 'tablename-foreign_tablename';
SET @table_name = 'tablename';

IF EXISTS (
    SELECT 1
    FROM information_schema.TABLE_CONSTRAINTS
    WHERE CONSTRAINT_TYPE = 'FOREIGN KEY'
      AND CONSTRAINT_NAME = @fk_name
      AND TABLE_NAME = @table_name
) THEN
    ALTER TABLE `tablename`
    DROP FOREIGN KEY `tablename-foreign_tablename`;
END IF;
```