---
title: Catálogo de banco de dados OLTP WideWorldImporters - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d98e87d18d76162e5bf9dcb4779a8bc7fec74385
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617617"
---
# <a name="wideworldimporters-database-catalog"></a>Catálogo de banco de dados de WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
O banco de dados de WideWorldImporters contém todos os as informações de transações e dados diários de vendas e compras, bem como dados de sensor para veículos e salas frias.

## <a name="schemas"></a>Esquemas

WideWorldImporters usa esquemas para finalidades diferentes, como armazenamento de dados, definindo como os usuários podem acessar os dados e fornecendo objetos para integração e desenvolvimento do data warehouse.

### <a name="data-schemas"></a>Esquemas de dados

Esses esquemas contenham os dados. Um número de tabelas é necessários para todos os outros esquemas e está localizado no esquema do aplicativo.

|esquema|Descrição|
|-----------------------------|---------------------|
|Aplicativo|Todo o aplicativo de usuários, contatos e parâmetros. Isso também contém tabelas de referência com dados que são usados por vários esquemas|
|Purchasing|Item de estoque compras de fornecedores e detalhes sobre fornecedores.|  
|Sales|Item vendas para clientes de varejo e detalhes sobre as pessoas de clientes e vendas do estoque. |  
|Warehouse|Estoque do item de estoque e transações.|  

### <a name="secure-access-schemas"></a>Esquemas de acesso seguro

Esses esquemas são usados para aplicativos externos que não têm permissão para acessar as tabelas de dados diretamente. Eles contêm exibições e procedimentos armazenados usados por aplicativos externos.

|esquema|Descrição|
|-----------------------------|---------------------|
|Site|Todo o acesso ao banco de dados do site da empresa é por meio desse esquema.|
|Relatórios|Todo o acesso ao banco de dados de relatórios do Reporting Services é por meio desse esquema.|
|PowerBI|Todo o acesso ao banco de dados de painéis do Power BI por meio do Gateway corporativo é por meio desse esquema.|

Observe que os relatórios e o Power BI esquemas não são usados na versão inicial do banco de dados de exemplo. No entanto, os exemplos do Reporting Services e o Power BI criados sobre esse banco de dados são incentivados a usar esses esquemas.

### <a name="development-schemas"></a>Esquemas de desenvolvimento

Esquemas de finalidade especial

|esquema|Descrição|
|-----------------------------|---------------------|
|Integração|Objetos e procedimentos necessários para a integração do depósito de dados (ou seja, migrando os dados para o banco de dados WideWorldImportersDW).|
|Sequências|Contém sequências usadas por todas as tabelas no aplicativo.|

## <a name="tables"></a>Tabelas

Todas as tabelas no banco de dados estão em esquemas de dados.

### <a name="application-schema"></a>Esquema do aplicativo

Detalhes de parâmetros e as pessoas (usuários e contatos), juntamente com as tabelas de referência comum (comuns a vários outras esquemas).

|Table|Descrição|
|-----------------------------|---------------------|
|SystemParameters|Contém os parâmetros configuráveis de todo o sistema.|
|Pessoas|Contém os nomes de usuário, informações de contato para todos que usam o aplicativo e para as pessoas que se trata da Wide World Importers em organizações do cliente. Isso inclui todos os outros contatos, clientes, fornecedores e equipe. Para as pessoas que receberam permissão para usar o sistema ou o site, as informações incluem detalhes de logon.|
|Cidades|Há muitos endereços armazenado no sistema, para as pessoas, endereços de entrega de organização do cliente, endereços de retirada em fornecedores, etc. Sempre que um endereço é armazenado, há uma referência a uma cidade nesta tabela. Também é um local espacial para cada cidade.|
|StateProvinces|Cidades fazem parte de estados ou províncias. Esta tabela tem detalhes deles, incluindo dados espaciais que descrevem os limites de cada estado ou província.|
|Países|Estados ou províncias fazem parte de países. Esta tabela tem detalhes deles, incluindo dados espaciais que descreve os limites de cada país.|
|DeliveryMethods|Escolhas para entregar os itens de estoque (por exemplo, caminhão/van, post, pickup, courier, etc.)|
|PaymentMethods|Opções para fazer pagamentos (por exemplo, o pagamento à vista, a verificação, TEF, etc.)|
|TransactionTypes|Tipos de cliente, fornecedor ou transações de estoque (por exemplo, nota fiscal, nota de crédito, etc.)|

### <a name="purchasing-schema"></a>Esquema de compra

Detalhes de fornecedores e de compras de item de estoque.

|Table|Descrição|
|-----------------------------|---------------------|
|Suppliers|Tabela de entidade principal para fornecedores (organizações)|
|SupplierCategories|Categorias de fornecedores (por exemplo, novelties, brinquedos, roupas, empacotamento, etc.)|
|SupplierTransactions|Todas as transações financeiras que são relacionados ao fornecedor (faturas, pagamentos)|
|PurchaseOrders|Detalhes de pedidos de compra de fornecedor|
|PurchaseOrderLines|Ordens de compra de linhas de detalhes de fornecedor|

 
### <a name="sales-schema"></a>Esquema de vendas

Detalhes de clientes, vendedores e das vendas do item de estoque.

|Table|Descrição|
|-----------------------------|---------------------|
|Customers|Tabelas de entidade principal para clientes (organizações ou indivíduos)|
|CustomerCategories|Categorias para os clientes (ou seja novidade armazenamentos, supermercados, etc.)|
|BuyingGroups|Organizações de clientes podem fazer parte de grupos que exercer maior potência de compra|
|CustomerTransactions|Todas as transações financeiras que são relacionadas ao cliente (faturas, pagamentos)|
|SpecialDeals|Preço especial. Isso pode incluir preços fixos, desconto em dólares ou porcentagem de desconto.|
|Orders|Detalhes de pedidos de clientes|
|OrderLines|Linhas de detalhes de pedidos do cliente|
|Notas fiscais|Detalhes de faturas de clientes|
|InvoiceLines|Linhas de detalhes de faturas do cliente|

### <a name="warehouse-schema"></a>Esquema de data warehouse

Detalhes de itens de estoque, holdings e transações.

|Table|Descrição|
|-----------------------------|---------------------|
|StockItems|Tabela de entidade principal para itens de estoque|
|StockItemHoldings|Colunas não temporal para itens de estoque. Essas são as colunas atualizadas com frequência.|
|StockGroups|Grupos para categorizar itens de estoque (por exemplo, novelties, brinquedos, novelties edible, etc.)|
|StockItemStockGroups|Quais itens de estoque são na qual o estoque grupos (muitos para muitos)|
|Cores|Itens de estoque (opcionalmente) podem ter cores|
|PackageTypes|Maneiras de itens de estoque podem ser empacotadas (por exemplo, caixa de papelão, palete, kg, etc.|
|StockItemTransactions|Transações que abrangem todos os movimentos de todos os itens de estoque (recebimento, venda, baixa)|
|VehicleTemperatures|Temperaturas gravadas regularmente do resfriadores do veículo|
|ColdRoomTemperatures|Registradas regularmente temperaturas de resfriadores sala frio|


## <a name="design-considerations"></a>Considerações de design

Design de banco de dados é subjetiva e não há nenhuma maneira certa ou errada de projetar um banco de dados. As tabelas neste banco de dados e esquemas mostram ideias de como você pode criar seu próprio banco de dados.

### <a name="schema-design"></a>Design de esquema

WideWorldImporters usa um pequeno número de esquemas para que seja fácil de entender o sistema de banco de dados e demonstram os princípios de banco de dados.  

Sempre que possível, o banco de dados coloca tabelas que normalmente são consultadas juntas no mesmo esquema para minimizar a complexidade de junção.

O esquema de banco de dados foi gerado pelo código com base em uma série de tabelas de metadados no banco de dados de outro WWI_Preparation. Assim, WideWorldImporters um grau muito alto de consistência de design, nomeação de consistência e integridade. Para obter detalhes sobre como o esquema tiver sido gerado, consulte o código-fonte: [todo o mundo-importadores/wwi-banco de dados-scripts](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>Design da tabela

- Todas as tabelas têm chaves primárias de coluna única para manter a simplicidade junção.
- Todos os esquemas, tabelas, colunas, índices e restrições de verificação tem uma descrição estendida de propriedade que pode ser usada para identificar a finalidade do objeto ou coluna. Tabelas com otimização de memória são uma exceção a isso, pois eles atualmente não dão suporte a propriedades estendidas.
- Todas as chaves estrangeiras são indexadas automaticamente, a menos que haja outro índice não clusterizado que tem o mesmo componente à esquerda.
- Numeração automática em tabelas com base em sequências. Essas sequências são mais fáceis de trabalhar em ambientes semelhantes do que as colunas de identidade e de servidores vinculados. Tabelas com otimização de memória usam colunas de identidade, pois eles não oferecem suporte no SQL Server 2016.
- Uma única sequência (TransactionID) é usada para essas tabelas: CustomerTransactions, SupplierTransactions e StockItemTransactions. Isso demonstra como um conjunto de tabelas pode ter uma única sequência.
- Algumas colunas tiverem valores padrão apropriados.

### <a name="security-schemas"></a>Esquemas de segurança

Para segurança, WideWorldImporters não permite aplicativos externos acessem diretamente os esquemas de dados. Para isolar o acesso, WideWorldImporters usa os esquemas de acesso de segurança que não contêm dados, mas contém exibições e procedimentos armazenados. Aplicativos externos usam os esquemas de segurança para recuperar os dados que eles têm permissão para exibir.  Dessa forma, os usuários podem apenas executar as exibições e procedimentos armazenados nos esquemas de acesso seguro

Por exemplo, este exemplo inclui painéis do Power BI. Um aplicativo externo acessa esses dashboards do Power BI do gateway do Power BI como um usuário que tem permissão somente leitura sobre o esquema do Power BI.  Permissão somente leitura, o usuário precisa apenas permissão SELECT e EXECUTE no esquema Power BI. Um administrador de banco de dados em WWI atribui essas permissões, conforme necessário.

## <a name="stored-procedures"></a>Procedimentos armazenados

Procedimentos armazenados são organizados em esquemas. A maioria dos esquemas é usada para fins de exemplo ou configuração.

O `Website` esquema contém os procedimentos armazenados que podem ser usados por um front-end da Web.

O `Reports` e `PowerBI` esquemas destinam-se para o reporting services e Power BI fins. Qualquer extensão de exemplo é incentivado a usar esses esquemas para fins de relatório.

### <a name="website-schema"></a>Esquema de site

Esses são os procedimentos usados por um aplicativo de cliente, como um front-end da Web.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|Permite que uma pessoa (de `Application.People`) para ter acesso ao site.|
|ChangePassword|Altera a senha do usuário (para usuários que não estão usando mecanismos de autenticação externos).|
|InsertCustomerOrders|Permite a inserção de uma ou mais ordens de cliente (incluindo as linhas da ordem).|
|InvoiceCustomerOrders|Usa uma lista de pedidos a ser faturada e processa as notas fiscais.|
|RecordColdRoomTemperatures|Usa uma lista de dados de sensor, como um parâmetro com valor de tabela (TVP) e aplica os dados para o `Warehouse.ColdRoomTemperatures` tabela temporal.|
|RecordVehicleTemperature|Usa uma matriz JSON e usa-o para atualizar `Warehouse.VehicleTemperatures`.|
|SearchForCustomers|Pesquisa os clientes por nome ou parte do nome (o nome da empresa ou o nome de pessoa).|
|SearchForPeople|Pesquisa de pessoas por nome ou parte do nome.|
|SearchForStockItems|Pesquisas de estoque itens por nome ou parte do nome ou comentários de marketing.|
|SearchForStockItemsByTags|Pesquisa itens estoque por marcas.|
|SearchForSuppliers|Procura por fornecedores por nome ou parte do nome (o nome da empresa ou o nome de pessoa).|

### <a name="integration-schema"></a>Esquema de integração

Os procedimentos armazenados neste esquema são usados pelo processo de ETL. Eles obtenham os dados necessários de várias tabelas para o período de tempo exigida pelo [pacote de ETL](wide-world-importers-perform-etl.md).

### <a name="dataloadsimulation-schema"></a>Esquema de DataLoadSimulation

Simula uma carga de trabalho que insere a vendas e compras. O procedimento armazenado principal é `PopulateDataToCurrentDate`, que é usado para inserir dados de exemplo até a data atual.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|Recria os procedimentos necessários para os dados de simulação carregar. Isso é necessário para colocar dados até a data atual.|
|Configuration_RemoveDataLoadSimulationProcedures|Isso remove os procedimentos novamente após a conclusão da simulação de dados.|
|DeactivateTemporalTablesBeforeDataLoad|Remove a natureza temporal de todas as tabelas temporais e onde aplicável, aplica um gatilho para que as alterações podem ser feitas, como se eles foram aplicados em uma data anterior não permita que as tabelas temporais de sys.|
|PopulateDataToCurrentDate|Usada para trazer os dados até a data atual. Deve ser executado antes de quaisquer outras opções de configuração depois de restaurar o banco de dados de um backup inicial.|
|ReactivateTemporalTablesAfterDataLoad|Restabelece as tabelas temporais, incluindo a verificação de consistência dos dados. (Remove os disparadores associados).|


### <a name="application-schema"></a>Esquema do aplicativo

Esses procedimentos são usados para configurar a amostra. Eles são usados para aplicar os recursos do enterprise edition para a versão de edição standard do exemplo e também adicionar auditoria e a indexação de texto completo.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|Adiciona um membro a uma função se o membro não estiver na função|
|Configuration_ApplyAuditing|Adiciona a auditoria. Auditoria de servidor é aplicado a bancos de dados standard edition; auditoria de banco de dados adicional é adicionado para o enterprise edition.|
|Configuration_ApplyColumnstoreIndexing|Aplica-se para a indexação de columnstore `Sales.OrderLines` e `Sales.InvoiceLines` e reindexará adequadamente.|
|Configuration_ApplyFullTextIndexing|Aplica-se a índices de texto completo para `Application.People`, `Sales.Customers`, `Purchasing.Suppliers`, e `Warehouse.StockItems`. Substitui `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers`, `Website.SearchForStockItems`, `Website.SearchForStockItemsByTags` com procedimentos de substituição que usam a indexação de texto completo.|
|Configuration_ApplyPartitioning|Aplica-se para o particionamento de tabela `Sales.CustomerTransactions and `'Purchasing.SupplierTransactions e reorganiza os índices de acordo com.|
|Configuration_ApplyRowLevelSecurity|Aplica segurança em nível de linha para filtrar os clientes por sales territory relacionadas a funções.|
|Configuration_ConfigureForEnterpriseEdition|Aplica-se a indexação de columnstore, texto completo, na memória, polybase e particionamento.|
|Configuration_EnableInMemory|Adiciona um grupo de arquivos com otimização de memória (quando não estiver trabalhando no Azure), substitui `Warehouse.ColdRoomTemperatures`, `Warehouse.VehicleTemperatures` com equivalentes na memória e migra os dados, recria o `Website.OrderIDList`, `Website.OrderList`, `Website.OrderLineList`, `Website.SensorDataList` com tipos de tabela equivalentes de otimização de memória, descarta e recria os procedimentos `Website.InvoiceCustomerOrders`, `Website.InsertCustomerOrders`, e `Website.RecordColdRoomTemperatures` que usa esses tipos de tabela.|
|Configuration_RemoveAuditing|Remove a configuração de auditoria.|
|Configuration_RemoveRowLevelSecurity|Remove a configuração de segurança em nível de linha (Isso é necessário para que as alterações às tabelas associadas).|
|CreateRoleIfNonExistant|Cria uma função de banco de dados se ele ainda não existir.|


### <a name="sequences-schema"></a>Esquema de sequências

Procedimentos para configurar as sequências no banco de dados.

|Procedimento|Finalidade|
|-----------------------------|---------------------|
|ReseedAllSequences|Chama o procedimento ReseedSequenceBeyondTableValue para todas as sequências.|
|ReseedSequenceBeyondTableValue|Usada para reposicionar o próximo valor de sequência além do valor em qualquer tabela que usa a mesma sequência. (Como um DBCC CHECKIDENT para equivalente de colunas de identidade para sequências, mas em potencialmente várias tabelas).|
