---
title: Catálogo de banco de dados OLAP WideWorldImporters - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 757820680533cfa2eaff8403e2056f0a4d3b1a96
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39556946"
---
# <a name="wideworldimportersdw-database-catalog"></a>Catálogo de banco de dados WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Explicações sobre os esquemas, tabelas e procedimentos armazenados no banco de dados WideWorldImportersDW. 

O banco de dados WideWorldImportersDW é usado para processamento analítico e de data warehouse. Os dados transacionais sobre vendas e compras são gerados no banco de dados de WideWorldImporters e carregados no banco de dados WideWorldImportersDW usando um **processo de ETL diário**.

Os dados em WideWorldImportersDW espelha, portanto, os dados de WideWorldImporters, mas as tabelas são organizadas de maneira diferente. Embora o WideWorldImporters tenha um esquema normalizado tradicional, WideWorldImportersDW usa o [esquema em estrela](https://wikipedia.org/wiki/Star_schema) abordagem para seu design de tabela. Além das tabelas de fatos e dimensão, o banco de dados inclui um número de tabelas de preparo que são usados no processo de ETL.

## <a name="schemas"></a>Esquemas

Os diferentes tipos de tabelas são organizados em três esquemas.

|esquema|Description|
|-----------------------------|---------------------|
|Dimensão|Tabelas de dimensões.|
|Fato|Tabelas de fatos.|  
|Integração|Tabelas de preparo e outros objetos necessários para ETL.|  

## <a name="tables"></a>Tabelas

As tabelas de dimensões e fatos são listadas abaixo. As tabelas no esquema de integração são usadas apenas para o processo de ETL e não estão listadas.

### <a name="dimension-tables"></a>Tabelas de dimensões

WideWorldImportersDW tem as seguintes tabelas de dimensões. A descrição inclui a relação com as tabelas de origem no banco de dados de WideWorldImporters.

|Table|Tabelas de origem|
|-----------------------------|---------------------|
|Cidade|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Cliente|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|data|Nova tabela com informações sobre as datas, incluindo o ano fiscal (com base em 1º de novembro Iniciar para o ano fiscal).|
|Employee|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|Fornecedor|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>Tabelas de fatos

WideWorldImportersDW tem as seguintes tabelas de fatos. A descrição inclui a relação com as tabelas de origem no banco de dados de WideWorldImporters, bem como as classes de consultas de análise/relatórios com que cada tabela de fatos é normalmente usada.

|Table|Tabelas de origem|Exemplo de análise|
|-----------------------------|---------------------|---------------------|
|Order|`Sales.Orders` e `Sales.OrderLines`|Produtividade de seletor/packer, as pessoas de vendas e no tempo para separar as ordens. Além disso, baixo estoque situações que levam a fazer pedidos.|
|Venda|`Sales.Invoices` e `Sales.InvoiceLines`|Datas de vendas, datas de entrega, lucratividade ao longo do tempo, lucratividade por vendedor.|
|Compra|`Purchasing.PurchaseOrderLines`|Prazos de entrega real de esperado vs|
|Transaction|`Sales.CustomerTransactions` e `Purchasing.SupplierTransactions`|Medindo o problema datas vs finalização datas e quantidades.|
|Movimentação|`Warehouse.StockTransactions`|Movimentações ao longo do tempo.|
|Ações|`Warehouse.StockItemHoldings`|Níveis de estoque disponível e o valor.|

## <a name="stored-procedures"></a>Procedimentos armazenados

Os procedimentos armazenados são usados principalmente para o processo de ETL e para fins de configuração.

Qualquer extensão de exemplo é incentivado a usar o `Reports` esquema de relatórios do Reporting Services e o `PowerBI` esquema para acesso ao Power BI.

### <a name="application-schema"></a>Esquema do aplicativo

Esses procedimentos são usados para configurar a amostra. Eles são usados para aplicar os recursos do enterprise edition para a versão standard edition do exemplo, adicione o PolyBase e propagar novamente o ETL.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|Aplica-se a índices de particionamento e o columnstore para tabelas de fatos.|
|Configuration_ConfigureForEnterpriseEdition|Aplica-se de particionamento, columnstore na memória e indexação.|
|Configuration_EnableInMemory|Substitui as tabelas de preparo de integração com as tabelas com otimização de memória SCHEMA_ONLY para melhorar o desempenho de ETL.|
|Configuration_ApplyPolybase|Configura uma fonte de dados externa, formato de arquivo e tabela.|
|Configuration_PopulateLargeSaleTable|Aplica as alterações do enterprise edition e, em seguida, preenche uma quantidade maior de dados para o ano de 2012 como histórico adicional.|
|Configuration_ReseedETL|Remove os dados existentes e reinicia as sementes ETL. Isso permite a repopulação do banco de dados OLAP para corresponder as linhas atualizadas no banco de dados OLTP.|

### <a name="integration-schema"></a>Esquema de integração

Os procedimentos usados no processo de ETL se enquadram nestas categorias:
- Procedimentos auxiliares para o pacote ETL - Get * todos os procedimentos.
- Os procedimentos usados pelo pacote de ETL para a migração de dados preparados nas tabelas de DW - todos os procedimentos de migração de *.
- `PopulateDateDimensionForYear` -Usa um ano e garante que todas as datas do ano são preenchidas no `Dimension.Date` tabela.

### <a name="sequences-schema"></a>Esquema de sequências

Procedimentos para configurar as sequências no banco de dados.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|ReseedAllSequences|Chama o procedimento `ReseedSequenceBeyondTableValue` para todas as sequências.|
|ReseedSequenceBeyondTableValue|Usada para reposicionar o próximo valor de sequência além do valor em qualquer tabela que usa a mesma sequência. (Como um `DBCC CHECKIDENT` para equivalente de colunas de identidade para sequências, mas em potencialmente várias tabelas.)|
