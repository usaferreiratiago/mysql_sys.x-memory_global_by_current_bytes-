# mysql_sys.x-memory_global_by_current_bytes-

SELECT 
    `performance_schema`.`memory_summary_global_by_event_name`.`EVENT_NAME` AS `event_name`,
    `performance_schema`.`memory_summary_global_by_event_name`.`CURRENT_COUNT_USED` AS `current_count`,
    `performance_schema`.`memory_summary_global_by_event_name`.`CURRENT_NUMBER_OF_BYTES_USED` AS `current_alloc`,
    IFNULL((`performance_schema`.`memory_summary_global_by_event_name`.`CURRENT_NUMBER_OF_BYTES_USED` / NULLIF(`performance_schema`.`memory_summary_global_by_event_name`.`CURRENT_COUNT_USED`,
                    0)),
            0) AS `current_avg_alloc`,
    `performance_schema`.`memory_summary_global_by_event_name`.`HIGH_COUNT_USED` AS `high_count`,
    `performance_schema`.`memory_summary_global_by_event_name`.`HIGH_NUMBER_OF_BYTES_USED` AS `high_alloc`,
    IFNULL((`performance_schema`.`memory_summary_global_by_event_name`.`HIGH_NUMBER_OF_BYTES_USED` / NULLIF(`performance_schema`.`memory_summary_global_by_event_name`.`HIGH_COUNT_USED`,
                    0)),
            0) AS `high_avg_alloc`
FROM
    `performance_schema`.`memory_summary_global_by_event_name`
WHERE
    (`performance_schema`.`memory_summary_global_by_event_name`.`CURRENT_NUMBER_OF_BYTES_USED` > 0)
ORDER BY `performance_schema`.`memory_summary_global_by_event_name`.`CURRENT_NUMBER_OF_BYTES_USED` DESC
