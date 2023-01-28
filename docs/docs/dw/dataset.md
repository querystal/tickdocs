Queries (Computing Tasks) are running on 0xTick streaming data warehouse. By following enterprise-level data warehouse practices, 0xTick data warehouse consists of three hirerachical layers, focusing on different grain levels of dataset.

## Layers
<b>Operational Data Store (ODS)</b>
> Operational data store has the original formats of datasets directly from blockchain full node, such as blocks, transactions, receipts, traces and logs. However, the original forms are semi-structured and encoded, leading to barriers of analysis via SQL queries, 0xTick refines the formats and structure of ODS tables, and usually users are less likely to use them often. 

<b>Data Warehouse Details (DWD)</b>
> Data warehouse details are batch of tables and views to form a general signals or bases of signals. They help users to focus on business analysis. 0xTick creates some DWD tables and views for users to start their works with trouble free.

<b>Application Rules (Rules)</b>
> In an enterprise-level data warehouse, application data store (ADS) are batch of tables and views serving application services. They are equavelant to Application Rules (Rules) in 0xTick. Any user query (SELECT statement) submitted via workspace is tagged with prefix of rule and considered an application rule.  

## ODS & DWD datasets
Official datasets are listed below:

|Layer|Table / View|Description|
|---|---|---|
|ODS|ods_eth_txns||
|ODS|ods_eth_blocks||
|ODS|ods_eth_receipts||
|ODS|ods_eth_logs||
|DWD|dwd_eth_cex_dim||
|DWD|dwd_eth_erc20_dim||
|DWD|dwd_eth_nft_dim||
|DWD|dwd_eth_erc20_event||
|DWD|dwd_eth_erc20_price||
|DWD|dwd_eht_ether_trades||
|DWD|dwd_eth_txn||
