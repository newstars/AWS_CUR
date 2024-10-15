### What columns are available in my Cost and Usage Report (CUR) file?
```
select * from {your_table_name}
where month(bill_billing_period_start_date) = 09 and year(bill_billing_period_start_date) = 2019 limit 10;
```

### What Billing periods are available?
```
SELECT distinct bill_billing_period_start_date FROM {your_table_name}
limit 12;
```

### Top 10 Costs by AWS Product
```
select "line_item_product_code", round(sum("line_item_unblended_cost"),2) as cost from {your_table_name}
where month(bill_billing_period_start_date) = 09 and year(bill_billing_period_start_date) = 2019
group by "line_item_product_code"
order by cost desc
limit 10;
```

### Top 20 Costs by Item Description and Tag “Project”
```
SELECT "bill_payer_account_id", "product_product_name", "line_item_usage_type", "line_item_line_item_description",
resource_tags_user_project, round(sum(line_item_unblended_cost),2) as cost FROM {your_table_name}
where length("resource_tags_user_project") >0 and month(bill_billing_period_start_date) = 09 and
year(bill_billing_period_start_date) = 2019
group by "resource_tags_user_project", "bill_payer_account_id", "product_product_name", "line_item_usage_type",
"line_item_line_item_description"
order by cost desc
limit 20;
```
