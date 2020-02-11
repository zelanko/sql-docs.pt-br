---
title: Catálogo de banco de dados OLAP do WideWorldImporters – SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 7c3da2af72743cc8f89273bfce24fe74fc7e4dc1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104295"
---
# <a name="wideworldimportersdw-database-catalog"></a>Catálogo de banco de dados WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Explicações para os esquemas, tabelas e procedimentos armazenados no banco de dados WideWorldImportersDW. 

O banco de dados WideWorldImportersDW é usado para processamento de data warehouse e analítico. Os dados transacionais sobre vendas e compras são gerados no banco de WideWorldImporters e carregados no banco de dados WideWorldImportersDW usando um **processo de ETL diário**.

Os dados em WideWorldImportersDW, portanto, espelham os dados em WideWorldImporters, mas as tabelas são organizadas de forma diferente. Embora o WideWorldImporters tenha um esquema normalizado tradicional, o WideWorldImportersDW usa a abordagem de [esquema em estrela](https://wikipedia.org/wiki/Star_schema) para seu design de tabela. Além das tabelas de fatos e de dimensões, o banco de dados inclui uma série de tabelas de preparo que são usadas no processo de ETL.

## <a name="schemas"></a>Esquemas

Os diferentes tipos de tabelas são organizados em três esquemas.

|Esquema|DESCRIÇÃO|
|-----------------------------|---------------------|
|Dimensão|Tabelas de dimensões.|
|Fato|Tabelas de fatos.|  
|Integração|Tabelas de preparo e outros objetos necessários para ETL.|  

## <a name="tables"></a>Tabelas

As tabelas de dimensões e fatos são listadas abaixo. As tabelas no esquema de integração são usadas apenas para o processo ETL e não são listadas.

### <a name="dimension-tables"></a>Tabelas de dimensões

WideWorldImportersDW tem as tabelas de dimensão a seguir. A descrição inclui a relação com as tabelas de origem no banco de dados WideWorldImporters.

|Tabela|Tabelas de origem|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Cliente|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|Data|Nova tabela com informações sobre datas, incluindo ano financeiro (com base em 1º de novembro de início para o ano financeiro).|
|Funcionário|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|Fornecedor|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>Tabelas de fatos

WideWorldImportersDW tem as seguintes tabelas de fatos. A descrição inclui a relação com as tabelas de origem no banco de dados WideWorldImporters, bem como as classes de consultas de análise/relatórios em que cada tabela de fatos é normalmente usada com o.

|Tabela|Tabelas de origem|Análise de exemplo|
|-----------------------------|---------------------|---------------------|
|Order|`Sales.Orders` e `Sales.OrderLines`|Vendedores, o seletor/produtividade do empacotador e no tempo para selecionar pedidos. Além disso, situações de ações baixas levando a pedidos pendentes.|
|Venda|`Sales.Invoices` e `Sales.InvoiceLines`|Datas de vendas, datas de entrega, rentabilidade ao longo do tempo, rentabilidade por vendedor.|
|Purchase|`Purchasing.PurchaseOrderLines`|Tempos de Lead reais esperados versus|
|Transação|`Sales.CustomerTransactions` e `Purchasing.SupplierTransactions`|Medindo datas de problemas vs. datas de finalização e valores.|
|Migração|`Warehouse.StockTransactions`|Movimentações ao longo do tempo.|
|Retenção de estoque|`Warehouse.StockItemHoldings`|Valores e níveis de estoque disponíveis.|

## <a name="stored-procedures"></a>Procedimentos armazenados

Os procedimentos armazenados são usados principalmente para o processo de ETL e para fins de configuração.

Todas as extensões do exemplo são incentivadas a usar `Reports` o esquema para Reporting Services relatórios e o `PowerBI` esquema para acesso do Power bi.

### <a name="application-schema"></a>Esquema do aplicativo

Esses procedimentos são usados para configurar o exemplo. Eles são usados para aplicar os recursos do Enterprise Edition à versão Standard Edition do exemplo, adicionar polybase e refazer a propagação do ETL.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|Aplica índices de particionamento e columnstore para tabelas de fatos.|
|Configuration_ConfigureForEnterpriseEdition|Aplica particionamento, indexação columnstore e na memória.|
|Configuration_EnableInMemory|Substitui as tabelas de preparo de integração por SCHEMA_ONLY tabelas com otimização de memória para melhorar o desempenho de ETL.|
|Configuration_ApplyPolyBase|Configura uma fonte de dados externa, um formato de arquivo e uma tabela.|
|Configuration_PopulateLargeSaleTable|Aplica as alterações do Enterprise Edition e, em seguida, popula uma quantidade maior de dados para o ano civil de 2012 como histórico adicional.|
|Configuration_ReseedETL|Remove os dados existentes e reinicia as sementes de ETL. Isso permite repopular o banco de dados OLAP para corresponder as linhas atualizadas no banco de dados OLTP.|

### <a name="integration-schema"></a>Esquema de integração

Os procedimentos usados no processo ETL se enquadram nessas categorias:
- Procedimentos auxiliares para o pacote ETL – todos os procedimentos Get *.
- Procedimentos usados pelo pacote ETL para migrar dados de preparo para as tabelas DW – todos os procedimentos Migrate *.
- `PopulateDateDimensionForYear`– Leva um ano e garante que todas as datas desse ano sejam preenchidas na `Dimension.Date` tabela.

### <a name="sequences-schema"></a>Esquema de sequências

Procedimentos para configurar as sequências no banco de dados.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|ReseedAllSequences|Chama o procedimento `ReseedSequenceBeyondTableValue` para todas as sequências.|
|ReseedSequenceBeyondTableValue|Usado para reposicionar o próximo valor de sequência além do valor em qualquer tabela que usa a mesma sequência. (Como uma `DBCC CHECKIDENT` coluna for Identity equivalente para Sequences, mas em potencialmente várias tabelas.)|
