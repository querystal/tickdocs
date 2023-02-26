Queries (Computing Tasks) are running on 0xTick streaming data warehouse. By following enterprise-level data warehouse practices, 0xTick data warehouse consists of three hirerachical layers, focusing on different grain levels of dataset.

## Layers
<b>Operational Data Store (ODS)</b>
> Operational data store has the original formats of datasets directly from blockchain full node, such as blocks, transactions, receipts, traces and logs. However, the original forms are semi-structured and encoded, leading to barriers of analysis via SQL queries, 0xTick refines the formats and structure of ODS tables, and usually users are less likely to use them directly. 

<b>Data Warehouse Details (DWD)</b>
> Data warehouse details are batch of tables and views to form a general signals or bases of signals. They help users to focus on business analysis. 0xTick creates some DWD tables and views for users to start their works with trouble free.

<b>Application Rules (Rules)</b>
> In an enterprise-level data warehouse, application data store (ADS) are batch of tables and views serving application services. They are equivalent to Application Rules (Rules) in 0xTick. Any query (SELECT statement) submitted via workspace is tagged with prefix of rule and considered an application rule.  

## ODS & DWD datasets
Official datasets are listed below:

|Layer|Table / View|Description|
|---|---|---|
|ODS|ods_eth_txns|all ethereum transactions with original format.|
|ODS|ods_eth_blocks|all ethereum blocks with original format.|
|ODS|ods_eth_receipts|all ethereum receipts of transactions with original format.|
|ODS|ods_eth_logs|all ethereum logs of transactions with original format.|
|DWD|dwd_eth_cex_dim|dimension table of centralised exchanges, including wallets and names.|
|DWD|dwd_eth_erc20_dim|dimension table of erc20 tokens, including scale of decimals and addresses.|
|DWD|dwd_eth_erc20_event|all erc20 operations, including deposit, withdrawl, transfer.|
|DWD|dwd_eth_erc20_price|real-time erc20 token prices in the market.|
|DWD|dwd_eth_ether_trades|all ether operations, including transfer, gas used, gas price.|
|DWD|dwd_eth_nft_event|nft trading events of major contracts, e.g. seaport.|
|DWD|dwd_eth_sync_progress_tab|the latest block number of ethereum synced by far.|
|DWD|dwd_eth_address_label|inhouse address labels provided by 0xTick.|

Datasets listed above are only the basic coverage as of now, please refer to meta station in [Event Studio][1] for the most up-to-date coverage.

[1]: <https://workspace.0xtick.com>