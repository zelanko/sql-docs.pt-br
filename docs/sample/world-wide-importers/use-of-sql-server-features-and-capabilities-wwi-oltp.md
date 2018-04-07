---
title: Uso de recursos do SQL Server | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
caps.latest.revision: 
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: 34535db5b43311e13d21fd663f5302327b24978e
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2018
---
# <a name="use-of-sql-server-features-and-capabilities"></a>Uso de recursos do SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters o uso de recursos do SQL Server e recursos no banco de dados OLTP.

WideWorldImporters é projetado para exibir muitos dos principais recursos do SQL Server, incluindo os recursos mais recentes introduzidos no SQL Server 2016. A seguir está uma lista de recursos do SQL Server, recursos e uma descrição de como eles são usados em WideWorldImporters.

|Recurso do SQL Server ou do recurso|Uso em WideWorldImporters|
|-----------------------------|---------------------|
|Tabelas temporais|Há muitas tabelas temporais, incluindo todas as tabelas de referência de estilo de pesquisa e principais entidades como StockItems, clientes e fornecedores. Permite usar tabelas temporais de forma conveniente controlar o histórico dessas entidades.|
|Chamadas AJAX para JSON|O aplicativo usa chamadas AJAX com frequência para consultar essas tabelas: pessoas, clientes, fornecedores e StockItems. As chamadas de retorno conteúdos JSON (ou seja, os dados que são retornados são formatados como dados JSON). Veja, por exemplo, o procedimento armazenado `Website.SearchForCustomers`.|
|Pacotes de propriedade/valor JSON|Um número de tabelas tem colunas que contêm dados JSON para estender os dados relacionais na tabela. Por exemplo, `Application.SystemParameters` tem uma coluna para as configurações do aplicativo e `Application.People` possui uma coluna para as preferências do usuário do registro. Essas tabelas usam um `nvarchar(max)` coluna para registrar os dados JSON, juntamente com uma restrição de verificação usando a função interna `ISJSON` para garantir que a coluna de valores são JSON válido.|
|Segurança de nível de linha (RLS)|Segurança de nível de linha (RLS) é usada para limitar o acesso à tabela de clientes, com base na associação de função. Cada região de vendas tem uma função e um usuário. Para ver isso em ação, use o script correspondente no exemplo-script.zip, que é parte do [versão do exemplo](http://go.microsoft.com/fwlink/?LinkID=800630).|
|Análise operacional em tempo real|(Versão completa do banco de dados) As tabelas transacional core `Sales.InvoiceLines` e `Sales.OrderLines` têm um índice columnstore não clusterizado para dar suporte a execução eficiente de consultas analíticas no banco de dados transacional com mínimo impacto na carga de trabalho operacional. Executar transações e análise no mesmo banco de dados também é conhecido como [de processamento de transacional/analítico híbrida (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP)). Para ver isso em ação, use o script correspondente no exemplo-script.zip, que é parte do [versão do exemplo](http://go.microsoft.com/fwlink/?LinkID=800630).|
|PolyBase|Para ver esse PolyBase em ação, usando uma tabela externa com um conjunto de dados público hospedado no armazenamento de blob do Azure, use o script correspondente no exemplo-script.zip, que faz parte do [versão do exemplo](http://go.microsoft.com/fwlink/?LinkID=800630).|
|OLTP na memória|(Versão completa do banco de dados) Os tipos de tabela são todos com otimização de memória, que com valor de tabela de parâmetros (TVPs) de todos os beneficiam da otimização de memória.<br/><br/>As duas tabelas de monitoramentos, `Warehouse.VehicleTemperatures` e `Warehouse.ColdRoomTemperatures`, tem otimização de memória. Isso permite que a tabela ColdRoomTemperatures preenchidos em velocidade superior de uma tabela tradicional baseada em disco. A tabela VehicleTemperatures contém a carga de JSON e se presta a extensão para cenários de IoT. A tabela VehicleTemperatures ainda mais se presta a cenários que envolvem EventHubs, análise de fluxo e Power BI.<br/><br/>O procedimento armazenado `Website.RecordColdRoomTemperatures` é compilado nativamente para melhorar ainda mais o desempenho de gravação de temperaturas frios.<br/><br/>Para ver um exemplo de OLTP na memória em ação, consulte o driver de carga de trabalho locais do veículo na carga de trabalho-drivers.zip, que é parte do [versão do exemplo](http://go.microsoft.com/fwlink/?LinkID=800630).|
|Índice columnstore clusterizado|(Versão completa do banco de dados) A tabela `Warehouse.StockItemTransactions` usa um índice columnstore clusterizado. O número de linhas nesta tabela é esperado aumentar e o índice columnstore clusterizado significativamente reduz o tamanho em disco da tabela e melhora o desempenho da consulta. A modificação nesta tabela são somente de inserção - não há nenhuma atualização/exclusão nesta tabela em uma carga de trabalho online - e índice columnstore clusterizado executa bem para cargas de trabalho de inserção.|
|Mascaramento de dados dinâmicos|No esquema de banco de dados, o mascaramento de dados tiver sido aplicado aos detalhes do banco mantidos por fornecedores, na tabela `Purchasing.Suppliers`. Equipe de não-administrador não terá acesso a essas informações.|
|Always Encrypted|Uma demonstração para sempre criptografado está incluída no Samples para download, que é parte do [versão do exemplo](http://go.microsoft.com/fwlink/?LinkID=800630)... A demonstração cria uma chave de criptografia, uma tabela usando a criptografia para dados confidenciais e um aplicativo de exemplo pequeno que insere dados na tabela.|
|O Stretch database|O `Warehouse.ColdRoomTemperatures` tabela tiver sido implementada como uma tabela temporal e tem otimização de memória na versão completa do banco de dados de exemplo. A tabela de arquivo morto é baseada em disco e pode ser esticada para o Azure.|
|Índices de texto completo|Índices de texto completo melhoram procura pessoas, clientes e StockItems. Os índices são aplicados a consultas somente se você tiver instalado na instância do SQL Server de indexação de texto completo. Uma coluna computada não persistente é usada para criar os dados que é o texto completo indexado na tabela StockItems.<br/><br/>`CONCAT` é usado para concatenar os campos para criar SearchData é indexada com texto completo.<br/>Para habilitar o uso de índices de texto completo no exemplo execute a seguinte instrução no banco de dados:<br/><br/>    `EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>O procedimento cria um catálogo de texto completo padrão se não existir, e substitui os modos de exibição de pesquisa com as versões de texto completo dessas exibições).<br/><br/>Observe que usando índices de texto completo no SQL Server requer a seleção da opção de texto completo durante a instalação. Não requer um banco de dados SQL do Azure e configuração específica para habilitar índices de texto completo.|
|Colunas computadas persistentes indexadas|Indexadas colunas computadas persistentes usadas em SupplierTransactions e CustomerTransactions.|
|Verificar restrições|É uma restrição de verificação relativamente complexo em `Sales.SpecialDeals`. Isso garante que um e somente um dos DiscountAmount, DiscountPercentage, e UnitPrice está configurado.|
|Restrições exclusivas|Um muitos para muitos construção (e restrições exclusivas) são configurados para Warehouse.StockItemStockGroups'.|
|O particionamento de tabela|(Versão completa do banco de dados) As tabelas `Sales.CustomerTransactions` e `Purchasing.SupplierTransactions` são particionados por ano usando a função de partição `PF_TransactionDate` e o esquema de partição `PS_TransactionDate`. O particionamento é usado para melhorar a capacidade de gerenciamento de grandes tabelas.|
|Processamento de lista|Um tipo de tabela de exemplo `Website.OrderIDList` é fornecido. Ele é usado por um procedimento de exemplo `Website.InvoiceCustomerOrders`. O procedimento usa a tabela CTEs (expressões comuns), TRY/CATCH, JSON_MODIFY, XACT_ABORT, NOCOUNT, THROW e XACT_STATE para demonstra a capacidade de processamento de uma lista de pedidos em vez de apenas uma única ordem, para minimizar as viagens de ida e do aplicativo para o mecanismo de banco de dados.|
|Compactação GZip|O `Warehouse.VehicleTemperature`tabela s contém dados de sensor completo, mas quando esses dados são mais do que alguns meses, ele é compactado para conservar o espaço usando a função COMPRESS, que usa compactação GZip.<br/><br/>O modo de exibição `Website.VehicleTemperatures` usa a função de descompactação ao recuperar dados que foi anteriormente compactados.|
|Repositório de Consultas|Repositório de consultas está habilitado no banco de dados. Depois de executar algumas consultas, abra o banco de dados no Management Studio, abra o nó do repositório de consultas, que está sob o banco de dados, e abrir o relatório principais consultas de consumo de recursos para ver as execuções de consulta e os planos para consultas que acabou de ser executada.|
|STRING_SPLIT|A coluna `DeliveryInstructions` na tabela `Sales.Invoices`tem um valor separado por vírgulas que pode ser usado para demonstrar STRING_SPLIT.|
|Auditar o|Auditoria do SQL Server pode ser habilitada para este banco de dados de exemplo, executando a seguinte instrução no banco de dados:<br/><br/>    `EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>No banco de dados SQL Azure, a auditoria é habilitada por meio de [portal do Azure](https://portal.azure.com/).<br/><br/>Operações de segurança que envolvem logons, funções e permissões são registradas em todos os sistemas onde a auditoria está habilitada (incluindo sistemas standard edition). Auditoria é direcionada para o log do aplicativo, porque isso está disponível em todos os sistemas e não requer permissões adicionais. Um aviso é visto que, para maior segurança, ele deve ser redirecionado para o log de segurança ou um arquivo em uma pasta segura. Um link é fornecido para descrever a configuração adicional necessária.<br/><br/>Para sistemas de desenvolvedor/avaliação/enterprise edition, o acesso a todos os dados transacionais financeiros é auditado.|
