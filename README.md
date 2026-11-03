# Data_modelling_project
Restructured a 23-table dataset with many-to-many relationships into a star schema with 6 dimensions and 6 fact
tables to support consistent reporting.

Built Power Query transformations (merges, splits, unpivots, and list expansion); removed test records, duplicates, and
unused fields, then validated control totals after tracing revenue fan-out to duplicate product records.

Created DAX measures for sales, distinct orders, active customers, and order-to-payment days; implemented regionbased row-level security using USERPRINCIPALNAME()
