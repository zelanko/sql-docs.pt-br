---
title: "Catálogo de banco de dados | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5ed65e42-527a-45e7-9a91-7179e892652e
caps.latest.revision: 2
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4205486c8e924471190221f19aca76554d4574b8
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="wideworldimportersdw-database-catalog"></a>Catálogo de banco de dados WideWorldImportersDW
Explicações para os esquemas, tabelas e procedimentos armazenados no banco de dados WideWorldImportersDW. 

O banco de dados WideWorldImportersDW é usado para processamento analítico e de data warehouse. Os dados transacionais sobre vendas e compras são gerados no banco de dados de WideWorldImporters e carregados no banco de dados WideWorldImportersDW usando um **processo ETL diário**.

Os dados em WideWorldImportersDW, portanto, reflete os dados de WideWorldImporters, mas as tabelas são organizadas de maneira diferente. Embora WideWorldImporters tem um esquema normalizado tradicional, WideWorldImportersDW usa o [esquema em estrela](https://wikipedia.org/wiki/Star_schema) abordagem para seu design de tabela. Além das tabelas de fatos e dimensões, o banco de dados inclui um número de tabelas de preparo que são usados no processo de ETL.

## <a name="schemas"></a>Esquemas

Os diferentes tipos de tabelas são organizados em três esquemas.

|Esquema|Description|
|-----------------------------|---------------------|
|Dimensão|Tabelas de dimensões.|
|Fato|Tabelas de fatos.|  
|Integração|Tabelas de preparo e outros objetos necessários para ETL.|  

## <a name="tables"></a>Tabelas

As tabelas de dimensões e fatos são listadas abaixo. As tabelas no esquema de integração são usadas somente para o processo ETL e não são listadas.

### <a name="dimension-tables"></a>Tabelas de dimensão

WideWorldImportersDW tem as seguintes tabelas de dimensões. A descrição inclui a relação com as tabelas de origem no banco de dados de WideWorldImporters.

|Table|Tabelas de origem|
|-----------------------------|---------------------|
|Cidade|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Cliente|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|Data|Nova tabela com informações sobre datas, incluindo o ano fiscal (com base em 1º de novembro Iniciar para ano fiscal).|
|Employee|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|Fornecedor|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>Tabelas de fatos

WideWorldImportersDW tem as seguintes tabelas de fatos. A descrição inclui a relação com as tabelas de origem no banco de dados de WideWorldImporters, bem como as classes de consultas/relatório de análise, com que cada tabela de fatos geralmente é usada.

|Table|Tabelas de origem|Análise de exemplo|
|-----------------------------|---------------------|---------------------|
|Order|`Sales.Orders`e`Sales.OrderLines`|Pessoas, produtividade de seletor/packer, de vendas e no tempo para separar as ordens. Além disso, baixa estoque situações que levam a fazer pedidos.|
|Venda|`Sales.Invoices`e`Sales.InvoiceLines`|Datas de vendas, datas de entrega, lucratividade ao longo do tempo, lucratividade por vendedor.|
|Compra|`Purchasing.PurchaseOrderLines`|Prazos de entrega real do vs esperado|
|Transaction|`Sales.CustomerTransactions`e`Purchasing.SupplierTransactions`|Medindo o problema datas vs finalização datas e valores.|
|Movimentação|`Warehouse.StockTransactions`|Movimentações ao longo do tempo.|
|Retenção de estoque|`Warehouse.StockItemHoldings`|Níveis de estoque disponível e o valor.|

## <a name="stored-procedures"></a>Procedimentos armazenados

Os procedimentos armazenados são usados principalmente para o processo de ETL e para fins de configuração.

Extensões do exemplo são incentivados a usar o `Reports` esquema para relatórios do Reporting Services e o `PowerBI` esquema para acesso ao Power BI.

### <a name="application-schema"></a>Esquema do aplicativo

Esses procedimentos são usados para configurar a amostra. Eles são usados para aplicar os recursos do enterprise edition para a versão standard edition do exemplo, adicione o PolyBase e propagar novamente ETL.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|Aplica o particionamento e columnstore índices para tabelas de fatos.|
|Configuration_ConfigureForEnterpriseEdition|Aplica o particionamento, columnstore na memória e indexação.|
|Configuration_EnableInMemory|Substitui as tabelas de preparo de integração com as tabelas com otimização de memória SCHEMA_ONLY para melhorar o desempenho de ETL.|
|Configuration_ApplyPolybase|Configura uma fonte de dados externa, o formato de arquivo e a tabela.|
|Configuration_PopulateLargeSaleTable|Aplicadas alterações de edição enterprise, em seguida, preenche uma quantidade maior de dados para o ano de 2012 como histórico adicional.|
|Configuration_ReseedETL|Remove os dados existentes e reinicia as propagações de ETL. Isso permite popular novamente o banco de dados OLAP para fazer a correspondência de linhas atualizadas no banco de dados OLTP.|

### <a name="integration-schema"></a>Esquema de integração

Os procedimentos usados no processo de ETL se enquadram nestas categorias:
- Procedimentos de auxiliar para o pacote ETL - Get * todos os procedimentos.
- Os procedimentos usados pelo pacote de ETL para migrar os dados preparados nas tabelas de DW - todos os procedimentos de migração de *.
- `PopulateDateDimensionForYear`-Usa um ano e garante que todas as datas que ano são preenchidas no `Dimension.Date` tabela.

### <a name="sequences-schema"></a>Esquema de sequências

Procedimentos para configurar as sequências no banco de dados.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|ReseedAllSequences|Chama o procedimento `ReseedSequenceBeyondTableValue` para todas as sequências.|
|ReseedSequenceBeyondTableValue|Usado para reposicionar o próximo valor de sequência além do valor em qualquer tabela que usa a mesma sequência. (Como um `DBCC CHECKIDENT` para equivalente de colunas de identidade para as sequências, mas em potencialmente várias tabelas).|

