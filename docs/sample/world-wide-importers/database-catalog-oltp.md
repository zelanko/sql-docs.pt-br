---
title: "Catálogo de banco de dados de WideWorldImporters | Microsoft Docs"
ms.prod: world-wide-importers
ms.prod_service: sql-non-specified
ms.service: samples
ms.component: 
ms.technology: samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e47c0022-ce87-4ba5-a24b-df55efe66431
caps.latest.revision: "3"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 4af23af22f369dc70110812b831e167b88b4885d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="wideworldimporters-database-catalog"></a>Catálogo de banco de dados de WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]O banco de dados de WideWorldImporters contém todas as a informações de transações e dados diário para compras e vendas, bem como dados de sensor de veículos e salas frios.

## <a name="schemas"></a>Esquemas

WideWorldImporters usa esquemas para finalidades diferentes, como armazenamento de dados, definir como os usuários podem acessar os dados e fornecer objetos de integração e desenvolvimento de depósito de dados.

### <a name="data-schemas"></a>Esquemas de dados

Esses esquemas contenham os dados. Um número de tabelas é necessárias para todos os outros esquemas e está localizado no esquema do aplicativo.

|esquema|Description|
|-----------------------------|---------------------|
|Aplicativo|Todo o aplicativo usuários, contatos e parâmetros. Isso também contém tabelas de referência com dados que são usados por vários esquemas|
|Purchasing|Item de estoque de compras de fornecedores e detalhes sobre fornecedores.|  
|Sales|Estoque item venda para clientes de varejo e detalhes sobre as pessoas de vendas e clientes. |  
|Warehouse|Inventário de item de estoque e transações.|  

### <a name="secure-access-schemas"></a>Esquemas de acesso seguro

Esses esquemas são usados para aplicativos externos que não têm permissão para acessar as tabelas de dados diretamente. Elas contêm exibições e procedimentos armazenados usados por aplicativos externos.

|esquema|Description|
|-----------------------------|---------------------|
|Site|Todo o acesso ao banco de dados do site da empresa é a este esquema.|
|Relatórios|Todo o acesso ao banco de dados de relatórios do Reporting Services é a este esquema.|
|Power BI|Todo o acesso ao banco de dados de painéis do Power BI por meio do Gateway corporativo é por este esquema.|

Observe que os relatórios e PowerBI esquemas não são usadas na versão inicial do banco de dados de exemplo. No entanto, os exemplos do Reporting Services e o Power BI criados sobre esse banco de dados são incentivados a usar esses esquemas.

### <a name="development-schemas"></a>Esquemas de desenvolvimento

Esquemas de finalidade especial

|esquema|Description|
|-----------------------------|---------------------|
|Integração|Objetos e procedimentos necessários para a integração do data warehouse (ou seja, migrando os dados para o banco de dados WideWorldImportersDW).|
|Sequências|Contém sequências usadas por todas as tabelas no aplicativo.|

## <a name="tables"></a>Tabelas

Todas as tabelas no banco de dados são nos esquemas de dados.

### <a name="application-schema"></a>Esquema do aplicativo

Detalhes de parâmetros e as pessoas (usuários e contatos), junto com as tabelas de referência comum (comuns a vários outros esquemas).

|Table|Description|
|-----------------------------|---------------------|
|SystemParameters|Contém os parâmetros configuráveis de todo o sistema.|
|Pessoas|Contém os nomes de usuário, informações de contato para todos os que usam o aplicativo e para as pessoas que trata a Wide World Importers em organizações de cliente. Isso inclui a funcionários, clientes, fornecedores e quaisquer outros contatos. Para as pessoas que receberam permissão para usar o sistema ou o site, as informações incluem detalhes de logon.|
|Cidades|Há muitos endereços armazenado no sistema, pessoas, endereços de entrega de organização de cliente, endereços de retirada em fornecedores, etc. Sempre que um endereço é armazenado, há uma referência a uma cidade nesta tabela. Também é um local espacial de cada cidade.|
|StateProvinces|Cidades fazem parte de estados ou províncias. Esta tabela tem detalhes deles, incluindo dados espaciais que descrevem os limites de cada estado ou província.|
|Países|Estados ou províncias fazem parte de países. Esta tabela tem detalhes deles, incluindo dados espaciais que descrevem os limites de cada país.|
|DeliveryMethods|Opções de entrega de itens de estoque (por exemplo, caminhão/van, post, retirada, courier, etc.)|
|PaymentMethods|Opções para fazer pagamentos (por exemplo, o dinheiro, a verificação, EFT, etc.)|
|TransactionTypes|Tipos de cliente, fornecedor ou transações de estoque (por exemplo, fatura, nota de crédito, etc.)|

### <a name="purchasing-schema"></a>Esquema de compra

Detalhes de fornecedores e de compras de item de estoque.

|Table|Description|
|-----------------------------|---------------------|
|Suppliers|Tabela de entidade principal de fornecedores (empresas)|
|SupplierCategories|Categorias de fornecedores (por exemplo, novelties, brinquedos, roupas, empacotamento, etc.)|
|SupplierTransactions|Todas as transações financeiras que são relacionados ao fornecedor (faturas, pagamentos)|
|PurchaseOrders|Detalhes de pedidos de compra do fornecedor|
|PurchaseOrderLines|Ordens de compra de linhas de detalhes de fornecedor|

 
### <a name="sales-schema"></a>Esquema de vendas

Detalhes de clientes, vendedores e de vendas de item de estoque.

|Table|Description|
|-----------------------------|---------------------|
|Customers|Tabelas de entidade principal para clientes (organizações ou pessoas físicas)|
|CustomerCategories|Categorias de clientes (ou seja novidade repositórios supermercados, etc.)|
|BuyingGroups|As organizações do cliente podem fazer parte de grupos de exercer maior capacidade de compra|
|CustomerTransactions|Todas as transações financeiras que estão relacionadas ao cliente (faturas, pagamentos)|
|SpecialDeals|Tipo de preço especiais. Isso pode incluir preços fixos, desconto em dólares ou porcentagem de desconto.|
|Orders|Detalhes de pedidos de clientes|
|OrderLines|Linhas de detalhes de pedidos de clientes|
|Faturas|Detalhes de faturas de clientes|
|InvoiceLines|Linhas de detalhes de faturas do cliente|

### <a name="warehouse-schema"></a>Esquema de data warehouse

Detalhes de itens de estoque, seus títulos e transações.

|Table|Description|
|-----------------------------|---------------------|
|StockItems|Tabela de entidade principal para itens de estoque|
|StockItemHoldings|Colunas não temporal para itens de estoque. Essas são as colunas atualizadas com frequência.|
|StockGroups|Grupos para categorizar itens de estoque (por exemplo, novelties toys, novelties edible, etc.)|
|StockItemStockGroups|Quais ações são na qual o estoque grupos (muitos para muitos)|
|Cores|Itens de estoque (opcionalmente) podem ter cores|
|PackageTypes|Maneiras de itens de estoque podem ser empacotadas (por exemplo, caixa de embalagem, paleta, kg, etc.|
|StockItemTransactions|Transações que abrangem todas as movimentações de todos os itens de estoque (recebimento, venda, baixa)|
|VehicleTemperatures|Temperaturas gravadas regularmente do resfriadores de veículo|
|ColdRoomTemperatures|Registrado regularmente temperaturas de resfriadores sala frios|


## <a name="design-considerations"></a>Considerações de design

Design de banco de dados é subjetiva e não é possível criar um banco de dados correto ou incorreto. As tabelas neste banco de dados e esquemas mostram obter ideias de como você pode criar seu próprio banco de dados.

### <a name="schema-design"></a>Design de esquema

WideWorldImporters usa um pequeno número de esquemas para que seja fácil de entender o sistema de banco de dados e demonstrar os princípios de banco de dados.  

Sempre que possível, o banco de dados collocates tabelas geralmente são consultadas juntos no mesmo esquema para minimizar a complexidade de junção.

O esquema de banco de dados foi gerado pelo código com base em uma série de tabelas de metadados em outro banco de dados WWI_Preparation. Assim, WideWorldImporters um grau muito alto de consistência de design, a consistência de nomenclatura e integridade. Para obter detalhes sobre como o esquema tiver sido gerado, consulte o código-fonte: [wide world-importadores/wwi-banco de dados-scripts](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>Design de tabela

- Todas as tabelas têm chaves primárias de coluna única para simplicidade de junção.
- Todos os esquemas, tabelas, colunas, índices e restrições de verificação tem uma descrição de propriedade que pode ser usada para identificar a finalidade do objeto ou coluna estendida. Tabelas com otimização de memória são uma exceção a isso, desde que eles não há suporte para propriedades estendidas.
- Todas as chaves estrangeiras são automaticamente indexadas, a menos que haja outro índice não clusterizado que tenha o mesmo componente à esquerda.
- Numeração automática em tabelas com base em sequências. Essas sequências são mais fáceis de trabalhar com servidores vinculados e ambientes semelhantes que as colunas de identidade. Tabelas com otimização de memória usam colunas de identidade, pois eles não dão suporte no SQL Server 2016.
- Uma única sequência (TransactionID) é usada para essas tabelas: CustomerTransactions, SupplierTransactions e StockItemTransactions. Isso demonstra como um conjunto de tabelas pode ter uma única sequência.
- Algumas colunas têm valores padrão apropriados.

### <a name="security-schemas"></a>Esquemas de segurança

Para segurança, WideWorldImporters não permite a aplicativos externos acessem diretamente os esquemas de dados. Para isolar o acesso, WideWorldImporters usa esquemas de acesso de segurança que não contêm dados, mas contém exibições e procedimentos armazenados. Aplicativos externos usam os esquemas de segurança para recuperar os dados que eles têm permissão para exibir.  Dessa forma, os usuários podem executar apenas as exibições e procedimentos armazenados nos esquemas de acesso seguro

Por exemplo, este exemplo inclui painéis do Power BI. Um aplicativo externo acessa esses painéis do Power BI do gateway do Power BI como um usuário que tem permissão somente leitura no esquema de Power BI.  Permissão somente leitura, o usuário só precisa de permissão SELECT e EXECUTE no esquema do Power BI. Um administrador de banco de dados em WWI atribui essas permissões conforme necessário.

## <a name="stored-procedures"></a>Procedimentos armazenados

Procedimentos armazenados são organizados em esquemas. A maioria dos esquemas é usada para fins de exemplo ou configuração.

O `Website` esquema contém os procedimentos armazenados que podem ser usados por um front-end da Web.

O `Reports` e `PowerBI` esquemas destinam-se para o reporting services e Power BI fins. Extensões do exemplo são incentivados a usar esses esquemas para fins de relatório.

### <a name="website-schema"></a>Esquema de site

Esses são os procedimentos usados por um aplicativo cliente, como um front-end da Web.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|Permite que uma pessoa (de `Application.People`) para ter acesso ao site.|
|ChangePassword|Altera a senha do usuário (para usuários que não estão usando os mecanismos de autenticação externa).|
|InsertCustomerOrders|Permite a inserção de um ou mais pedidos de clientes (incluindo as linhas de ordem).|
|InvoiceCustomerOrders|Usa uma lista de pedidos por ser faturado e processa as faturas.|
|RecordColdRoomTemperatures|Usa uma lista de dados de sensor, como um parâmetro com valor de tabela (TVP) e aplica os dados para o `Warehouse.ColdRoomTemperatures` tabela temporal.|
|RecordVehicleTemperature|Leva uma matriz JSON e usa-o para atualizar `Warehouse.VehicleTemperatures`.|
|SearchForCustomers|Pesquisa de clientes por nome ou parte do nome (o nome da empresa ou o nome da pessoa).|
|SearchForPeople|Procura por pessoas por nome ou parte do nome.|
|SearchForStockItems|Pesquisas de estoque itens por nome ou parte do nome ou comentários de marketing.|
|SearchForStockItemsByTags|Pesquisa para itens de estoque por marcas.|
|SearchForSuppliers|Procura por fornecedores por nome ou parte do nome (o nome da empresa ou o nome da pessoa).|

### <a name="integration-schema"></a>Esquema de integração

Os procedimentos armazenados nesse esquema são usados pelo processo de ETL. Obter os dados necessários de várias tabelas para o período de tempo necessário para o [pacote ETL](etl-workflow.md).

### <a name="dataloadsimulation-schema"></a>Esquema de DataLoadSimulation

Simula uma carga de trabalho que insere vendas e compras. O procedimento armazenado principal é `PopulateDataToCurrentDate`, que é usado para inserir dados de exemplo até a data atual.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|Recria os procedimentos necessários para dados de simulação carga. Isso é necessário para colocar dados até a data atual.|
|Configuration_RemoveDataLoadSimulationProcedures|Isso remove os procedimentos novamente após a conclusão da simulação de dados.|
|DeactiveTemporalTablesBeforeDataLoad|Remove a natureza temporal de todas as tabelas temporais e onde aplicável, aplica um gatilho para que as alterações podem ser feitas como se eles foram aplicados em uma data anterior de permitir que as tabelas temporais de sys.|
|PopulateDataToCurrentDate|Usado para colocar os dados até a data atual. Deve ser executado antes de quaisquer outras opções de configuração depois de restaurar o banco de dados de um backup inicial.|
|ReactivateTemporalTablesAfterDataLoad|Restabelece as tabelas temporais, incluindo a verificação de consistência de dados. (Remove os disparadores associados).|


### <a name="application-schema"></a>Esquema do aplicativo

Esses procedimentos são usados para configurar a amostra. Eles são usados para aplicar os recursos do enterprise edition para a versão standard edition do exemplo e também adicionar auditoria e indexação de texto completo.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|Adiciona um membro a uma função se o membro não estiver na função|
|Configuration_ApplyAuditing|Adiciona a auditoria. Auditoria de servidor é aplicada para bancos de dados standard edition; auditoria de banco de dados adicional é adicionada para o enterprise edition.|
|Configuration_ApplyColumnstoreIndexing|Aplica-se columnstore indexação a `Sales.OrderLines` e `Sales.InvoiceLines` e reindexes adequadamente.|
|Configuration_ApplyFullTextIndexing|Aplica-se a índices de texto completo para `Application.People`, `Sales.Customers`, `Purchasing.Suppliers`, e `Warehouse.StockItems`. Substitui `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers`, `Website.SearchForStockItems`, `Website.SearchForStockItemsByTags` com os procedimentos de substituição que usam a indexação de texto completo.|
|Configuration_ApplyPartitioning|Aplica o particionamento de tabela para `Sales.CustomerTransactions and `'Purchasing.SupplierTransactions e reorganizar os índices de acordo com.|
|Configuration_ApplyRowLevelSecurity|Se aplica a segurança em nível de linha para filtrar os clientes por vendas território relacionadas a funções.|
|Configuration_ConfigureForEnterpriseEdition|Aplica-se a indexação de columnstore, texto completo, na memória, polybase e particionamento.|
|Configuration_EnableInMemory|Adiciona um grupo de arquivos com otimização de memória (quando não estiver trabalhando no Azure), substitui `Warehouse.ColdRoomTemperatures`, `Warehouse.VehicleTemperatures` com equivalentes na memória e migra os dados, recria o `Website.OrderIDList`, `Website.OrderList`, `Website.OrderLineList`, `Website.SensorDataList` tipos de tabela com otimização de memória equivalentes, descarta e recria os procedimentos `Website.InvoiceCustomerOrders`, `Website.InsertCustomerOrders`, e `Website.RecordColdRoomTemperatures` que usa esses tipos de tabela.|
|Configuration_RemoveAuditing|Remove a configuração de auditoria.|
|Configuration_RemoveRowLevelSecurity|Remove a configuração de segurança em nível de linha (Isso é necessário para que as alterações às tabelas associadas).|
|CreateRoleIfNonExistant|Cria uma função de banco de dados se ele ainda não existir.|


### <a name="sequences-schema"></a>Esquema de sequências

Procedimentos para configurar as sequências no banco de dados.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|ReseedAllSequences|Chama o procedimento ReseedSequenceBeyondTableValue para todas as sequências.|
|ReseedSequenceBeyondTableValue|Usado para reposicionar o próximo valor de sequência além do valor em qualquer tabela que usa a mesma sequência. (Como um DBCC CHECKIDENT para equivalente de colunas de identidade para as sequências, mas em potencialmente várias tabelas).|
