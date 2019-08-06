---
title: Catálogo de banco de dados OLTP WideWorldImporters-SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2560043ca6acc4b5df141bcbc898ac09b21f97a8
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811534"
---
# <a name="wideworldimporters-database-catalog"></a>Catálogo de banco de dados WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
O banco de dados do WideWorldImporters contém todas as informações de transação e de venda diárias para vendas e compras, bem como dados de sensor para veículos e quartos frios.

## <a name="schemas"></a>Esquemas

O WideWorldImporters usa esquemas para finalidades diferentes, como armazenar dados, definir como os usuários podem acessar os dados e fornecer objetos para desenvolvimento e integração de data warehouse.

### <a name="data-schemas"></a>Esquemas de dados

Esses esquemas contêm os dados. Várias tabelas são necessárias para todos os outros esquemas e estão localizadas no esquema do aplicativo.

|Esquema|Descrição|
|-----------------------------|---------------------|
|Aplicativo|Usuários, contatos e parâmetros de todo o aplicativo. Isso também contém tabelas de referência com dados que são usados por vários esquemas|
|Purchasing|Compras de itens de estoque de fornecedores e detalhes sobre fornecedores.|  
|Sales|Vendas de itens de estoque para clientes de varejo e detalhes sobre clientes e pessoas de vendas. |  
|Warehouse|Estoque de item de estoque e transações.|  

### <a name="secure-access-schemas"></a>Esquemas de acesso seguro

Esses esquemas são usados para aplicativos externos que não têm permissão para acessar as tabelas de dados diretamente. Eles contêm exibições e procedimentos armazenados usados por aplicativos externos.

|Esquema|Descrição|
|-----------------------------|---------------------|
|Site|Todo o acesso ao banco de dados do site da empresa é por meio desse esquema.|
|Relatórios|Todo o acesso ao banco de dados de Reporting Services relatórios é por meio desse esquema.|
|PowerBI|Todo o acesso ao banco de dados do Power BI dashboards por meio do gateway corporativo é por meio desse esquema.|

Observe que os esquemas de relatórios e PowerBI não são usados na versão inicial do banco de dados de exemplo. No entanto, todos os Reporting Services e Power BI amostras criadas sobre esse banco de dados são incentivados a usar esses esquemas.

### <a name="development-schemas"></a>Esquemas de desenvolvimento

Esquemas de finalidade especial

|Esquema|Descrição|
|-----------------------------|---------------------|
|Integração|Objetos e procedimentos necessários para a integração do data warehouse (ou seja, migrar os dados para o banco de WideWorldImportersDW).|
|Sequências|Armazena as sequências usadas por todas as tabelas no aplicativo.|

## <a name="tables"></a>Tabelas

Todas as tabelas no banco de dados estão nos esquemas de data.

### <a name="application-schema"></a>Esquema do aplicativo

Detalhes de parâmetros e pessoas (usuários e contatos), juntamente com tabelas de referência comuns (comuns a vários outros esquemas).

|Tabela|Descrição|
|-----------------------------|---------------------|
|Sistemaparameters|Contém parâmetros configuráveis para todo o sistema.|
|Porta|Contém nomes de usuário, informações de contato, para todos os que usam o aplicativo e para as pessoas que a Wide World Importers lidam em organizações de clientes. Isso inclui a equipe, os clientes, os fornecedores e outros contatos. Para pessoas que receberam permissão para usar o sistema ou site, as informações incluem detalhes de logon.|
|Primeiras|Há muitos endereços armazenados no sistema, para pessoas, endereços de entrega da organização do cliente, endereços de retirada em fornecedores, etc. Sempre que um endereço é armazenado, há uma referência a uma cidade nesta tabela. Também há um local espacial para cada cidade.|
|StateProvinces|As cidades fazem parte de Estados ou províncias. Esta tabela tem detalhes daqueles, incluindo dados espaciais que descrevem os limites de cada Estado ou província.|
|Países|Estados ou províncias são parte dos países. Esta tabela tem detalhes daqueles, incluindo dados espaciais que descrevem os limites de cada país.|
|DeliveryMethods|Opções para entrega de itens de estoque (por exemplo, caminhão/Van, post, pickup, Courier, etc.)|
|PaymentMethods|Opções para fazer pagamentos (por exemplo, caixa, cheque, TEF, etc.)|
|TransactionTypes|Tipos de transações de cliente, fornecedor ou estoque (por exemplo, fatura, nota de crédito etc.)|

### <a name="purchasing-schema"></a>Esquema de compra

Detalhes de fornecedores e compras de itens de estoque.

|Tabela|Descrição|
|-----------------------------|---------------------|
|Fornecedores|Tabela principal de entidades para fornecedores (organizações)|
|SupplierCategories|Categorias para fornecedores (por exemplo, Novelties, brinquedos, roupas, empacotamento etc.)|
|SupplierTransactions|Todas as transações financeiras que são relacionadas ao fornecedor (faturas, pagamentos)|
|PurchaseOrders|Detalhes de pedidos de compra do fornecedor|
|PurchaseOrderLines|Linhas de detalhes de ordens de compra do fornecedor|

 
### <a name="sales-schema"></a>Esquema de vendas

Detalhes de clientes, vendedores e vendas de itens de estoque.

|Tabela|Descrição|
|-----------------------------|---------------------|
|Customers|Tabelas de entidade principal para clientes (organizações ou indivíduos)|
|CustomerCategories|Categorias para clientes (do IE novidade lojas, supermercados, etc.)|
|BuyingGroups|As organizações de clientes podem fazer parte de grupos que exercem maior poder de compra|
|CustomerTransactions|Todas as transações financeiras relacionadas ao cliente (faturas, pagamentos)|
|SpecialDeals|Preços especiais. Isso pode incluir preços fixos, desconto em dólares ou percentual de desconto.|
|Orders|Detalhe de pedidos de clientes|
|OrderLines|Linhas de detalhes de pedidos de clientes|
|Faturas|Detalhes de notas fiscais de clientes|
|InvoiceLines|Linhas de detalhes de notas fiscais do cliente|

### <a name="warehouse-schema"></a>Esquema do warehouse

Detalhes de itens de estoque, seus ententos e transações.

|Tabela|Descrição|
|-----------------------------|---------------------|
|StockItems|Tabela principal de entidade para itens de estoque|
|StockItemHoldings|Colunas não temporais para itens de estoque. Essas são colunas atualizadas com frequência.|
|StockGroups|Grupos para categorização de itens de estoque (por exemplo, Novelties, Toys, edible Novelties, etc.)|
|StockItemStockGroups|Quais itens de estoque estão em quais grupos de ações (muitos para muitos)|
|Cores|Os itens de estoque podem (opcionalmente) ter cores|
|PackageTypes|Maneiras como os itens de estoque podem ser empacotados (por exemplo, caixa, cartão, palete, kg, etc.)|
|StockItemTransactions|Transações que abrangem todos os movimentos de todos os itens de estoque (recebimento, venda, gravação)|
|VehicleTemperatures|Temperaturas regularmente registradas de resfriadores de veículo|
|ColdRoomTemperatures|Temperaturas regularmente registradas de resfriadores de sala frio|


## <a name="design-considerations"></a>Considerações de design

O design do banco de dados está sujeito e não há uma maneira correta ou errada de criar um banco de dados. Os esquemas e as tabelas neste banco de dados mostram ideias sobre como você pode criar seu próprio banco de dados.

### <a name="schema-design"></a>Design de esquema

O WideWorldImporters usa um pequeno número de esquemas para que seja fácil entender o sistema de banco de dados e demonstrar princípios de banco de dados.  

Sempre que possível, o banco de dados coloca tabelas que geralmente são consultadas juntas no mesmo esquema para minimizar a complexidade da junção.

O esquema de banco de dados foi gerado pelo código com base em uma série de tabelas de metadados em outro banco de dados WWI_Preparation. Isso dá ao WideWorldImporters um grau muito alto de consistência de design, consistência de nomenclatura e integridade. Para obter detalhes sobre como o esquema foi gerado, consulte o código-fonte: [Wide-World-outporters/WWI-Database-scripts](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>Design de tabela

- Todas as tabelas têm chaves primárias de coluna única para a simplicidade de junção.
- Todos os esquemas, tabelas, colunas, índices e restrições de verificação têm uma propriedade estendida de descrição que pode ser usada para identificar a finalidade do objeto ou da coluna. As tabelas com otimização de memória são uma exceção a isso, pois atualmente não dão suporte a propriedades estendidas.
- Todas as chaves estrangeiras são indexadas automaticamente, a menos que haja outro índice não clusterizado que tenha o mesmo componente do lado esquerdo.
- A numeração automática em tabelas é baseada em sequências. Essas sequências são mais fáceis de trabalhar com servidores vinculados e ambientes semelhantes que as colunas de identidade. As tabelas com otimização de memória usam colunas de identidade, pois não oferecem suporte no SQL Server 2016.
- Uma única sequência (TransactionId) é usada para essas tabelas: CustomerTransactions, SupplierTransactions e StockItemTransactions. Isso demonstra como um conjunto de tabelas pode ter uma única sequência.
- Algumas colunas têm valores padrão apropriados.

### <a name="security-schemas"></a>Esquemas de segurança

Por segurança, o WideWorldImporters não permite que aplicativos externos acessem esquemas de dados diretamente. Para isolar o acesso, o WideWorldImporters usa esquemas de acesso de segurança que não contêm dados, mas contêm exibições e procedimentos armazenados. Os aplicativos externos usam os esquemas de segurança para recuperar os dados que eles têm permissão para exibir.  Dessa forma, os usuários só podem executar os modos de exibição e procedimentos armazenados nos esquemas de acesso seguro

Por exemplo, este exemplo inclui Power BI Dashboards. Um aplicativo externo acessa esses Power BI dashboards do gateway de Power BI como um usuário que tem permissão somente leitura no esquema do PowerBI.  Para permissão somente leitura, o usuário precisa apenas da permissão SELECT e EXECUTE no esquema do PowerBI. Um administrador de banco de dados em WWI atribui essas permissões conforme necessário.

## <a name="stored-procedures"></a>Procedimentos armazenados

Os procedimentos armazenados são organizados em esquemas. A maioria dos esquemas é usada para fins de configuração ou de exemplo.

O `Website` esquema contém os procedimentos armazenados que podem ser usados por um front-end da Web.

Os `Reports` esquemas `PowerBI` e são destinados a fins do Reporting Services e do PowerBI. Todas as extensões do exemplo são incentivadas a usar esses esquemas para fins de relatório.

### <a name="website-schema"></a>Esquema de site

Esses são os procedimentos usados por um aplicativo cliente, como um front-end da Web.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|Permite que uma pessoa ( `Application.People`de) tenha acesso ao site.|
|ChangePassword|Altera a senha de um usuário (para usuários que não estão usando mecanismos de autenticação externa).|
|InsertCustomerOrders|Permite inserir um ou mais pedidos de clientes (incluindo as linhas de ordem).|
|InvoiceCustomerOrders|Usa uma lista de pedidos a serem faturados e processa as notas fiscais.|
|RecordColdRoomTemperatures|Usa uma lista de dados de sensor, como um parâmetro com valor de tabela (TVP) e aplica os dados `Warehouse.ColdRoomTemperatures` à tabela temporal.|
|RecordVehicleTemperature|Usa uma matriz JSON e a utiliza para atualizar `Warehouse.VehicleTemperatures`.|
|SearchForCustomers|Procura clientes por nome ou por parte do nome (o nome da empresa ou o nome da pessoa).|
|SearchForPeople|Pesquisa pessoas por nome ou parte do nome.|
|SearchForStockItems|Procura itens de ações por nome ou por parte do nome ou de comentários de marketing.|
|SearchForStockItemsByTags|Procura itens de ações por marcas.|
|SearchForSuppliers|Procura fornecedores por nome ou por parte do nome (o nome da empresa ou o nome da pessoa).|

### <a name="integration-schema"></a>Esquema de integração

Os procedimentos armazenados neste esquema são usados pelo processo de ETL. Eles obtêm os dados necessários de várias tabelas para o período de tempo exigido pelo [pacote ETL](wide-world-importers-perform-etl.md).

### <a name="dataloadsimulation-schema"></a>Esquema DataLoadSimulation

Simula uma carga de trabalho que insere vendas e compras. O procedimento armazenado principal é `PopulateDataToCurrentDate`, que é usado para inserir dados de exemplo até a data atual.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|Recria os procedimentos necessários para a simulação de carregamento de dados. Isso é necessário para trazer dados até a data atual.|
|Configuration_RemoveDataLoadSimulationProcedures|Isso removerá os procedimentos novamente após a conclusão da simulação de dados.|
|DeactivateTemporalTablesBeforeDataLoad|Remove a natureza temporal de todas as tabelas temporais e, quando aplicável, aplica um gatilho para que as alterações possam ser feitas como se estivessem sendo aplicadas em uma data anterior ao que as tabelas sys-temporal permitem.|
|PopulateDataToCurrentDate|Usado para trazer os dados até a data atual. Deve ser executado antes de qualquer outra opção de configuração depois de restaurar o banco de dados a partir de um backup inicial.|
|ReactivateTemporalTablesAfterDataLoad|Restabelece as tabelas temporais, incluindo a verificação de consistência de dados. (Remove os gatilhos associados).|


### <a name="application-schema"></a>Esquema do aplicativo

Esses procedimentos são usados para configurar o exemplo. Eles são usados para aplicar os recursos do Enterprise Edition à versão Standard Edition do exemplo e também para adicionar auditoria e indexação de texto completo.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|Adiciona um membro a uma função se o membro ainda não estiver na função|
|Configuration_ApplyAuditing|Adiciona auditoria. A auditoria de servidor é aplicada a bancos de dados Standard Edition; a auditoria de banco de dados adicional é adicionada para a Enterprise Edition.|
|Configuration_ApplyColumnstoreIndexing|Aplica a indexação columnstore `Sales.OrderLines` para `Sales.InvoiceLines` e e reindexe adequadamente.|
|Configuration_ApplyFullTextIndexing|Aplica índices de texto `Application.People`completo `Sales.Customers`a `Purchasing.Suppliers`,, `Warehouse.StockItems`e. Substitui `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers` ,,porprocedimentosdesubstituiçãoqueusamindexaçãodetextocompleto.`Website.SearchForStockItemsByTags` `Website.SearchForStockItems`|
|Configuration_ApplyPartitioning|Aplica o particionamento de tabela `Sales.CustomerTransactions` para `Purchasing.SupplierTransactions`e e reorganiza os índices para adaptá-los.|
|Configuration_ApplyRowLevelSecurity|Aplica a segurança em nível de linha para filtrar clientes por funções relacionadas à região de vendas.|
|Configuration_ConfigureForEnterpriseEdition|Aplica indexação columnstore, texto completo, na memória, polybase e particionamento.|
|Configuration_EnableInMemory|Adiciona um grupo de arquivos com otimização de memória (quando não estiver trabalhando no Azure `Warehouse.ColdRoomTemperatures`) `Warehouse.VehicleTemperatures` , substitui, por equivalentes na memória, e migra os dados, `Website.OrderLineList`recria os `Website.OrderIDList`tipos `Website.OrderList`de tabela `Website.SensorDataList` ,,, com equivalentes com otimização de memória, descarta e recria os procedimentos `Website.InvoiceCustomerOrders`, `Website.InsertCustomerOrders`e `Website.RecordColdRoomTemperatures` que usa esses tipos de tabela.|
|Configuration_RemoveAuditing|Remove a configuração de auditoria.|
|Configuration_RemoveRowLevelSecurity|Remove a configuração de segurança em nível de linha (necessária para alterações nas tabelas associadas).|
|CreateRoleIfNonExistant|Cria uma função de banco de dados, caso ela ainda não exista.|


### <a name="sequences-schema"></a>Esquema de sequências

Procedimentos para configurar as sequências no banco de dados.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|ReseedAllSequences|Chama o procedimento ReseedSequenceBeyondTableValue para todas as sequências.|
|ReseedSequenceBeyondTableValue|Usado para reposicionar o próximo valor de sequência além do valor em qualquer tabela que usa a mesma sequência. (Como uma DBCC CHECKIDENT para colunas de identidade equivalentes para sequências, mas em potencialmente várias tabelas).|
