---
title: Banco de dados tempdb - Parallel Data Warehouse | Microsoft Docs
description: Banco de dados tempdb em Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7e11f4eff980358f4b4906f8a100cfc509d19dd5
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>banco de dados tempdb em Parallel Data Warehouse
**tempdb** é um banco de dados de sistema do PDW do SQL Server que armazena as tabelas temporárias locais para bancos de dados do usuário. Tabelas temporárias são geralmente usadas para melhorar o desempenho da consulta. Por exemplo, você pode usar uma tabela temporária para modularizar um script e reutilizar os dados computados.  
  
Para obter mais informações sobre bancos de dados do sistema, consulte [bancos de dados do sistema](system-databases.md).  
  
## <a name="Basics"></a>Termos e conceitos essenciais  
*tabela temporária local*  
Um *tabela temporária local* usa o prefixo # antes do nome da tabela e é uma tabela temporária criada por uma sessão de usuário local. Cada sessão só pode acessar os dados em tabelas temporárias locais para sua própria sessão.  
  
Cada sessão pode exibir os metadados para tabelas temporárias locais em todas as sessões. Por exemplo, todas as sessões podem exibir os metadados para todas as tabelas temporárias locais com o `SELECT * FROM tempdb.sys.tables` consulta.  
  
tabela temporária global  
*Tabelas temporárias globais*, com suporte no SQL Server com o # # sintaxe, não há suporte para esta versão do SQL Server PDW.  
  
pdwtempdb  
**pdwtempdb** o banco de dados que armazena a tabelas temporárias locais.  
  
PDW não implementa tabelas temporárias usando o SQL Server**tempdb** banco de dados. Em vez disso, PDW armazena em um banco de dados chamado pdwtempdb. Este banco de dados existe em cada nó de computação e invisível para o usuário por meio das interfaces do PDW. No Console do administrador, na página de armazenamento, você verá esses contabilizado para em um banco de dados do sistema do PDW chamado **tempdb sql**.  
  
tempdb  
**tempdb** é o banco de dados do tempdb do SQL Server. Ele usa o log mínimo. SQL Server usa o tempdb em nós de computação para armazenar tabelas temporárias necessárias durante a execução de operações do SQL Server.  
  
SQL Server PDW descarta tabelas de **tempdb** quando:  
  
-   A instrução DROP TABLE for executada.  
  
-   Uma sessão é desconectada. Somente as tabelas temporárias para a sessão serão descartadas.  
  
-   O dispositivo é desligado.  
  
-   O nó de controle tem um cluster de failover.  
  
## <a name="general-remarks"></a>Comentários gerais  
SQL Server PDW executa as mesmas operações em tabelas temporárias e tabelas permanentes, a menos que explicitamente indicado em contrário. Por exemplo, os dados em tabelas temporárias locais, como tabelas permanentes, está distribuídos ou replicados em todos os nós de computação.  
  
## <a name="LimitationsRestrictions"></a>Limitações e restrições  
Limitações e restrições sobre o SQL Server PDW**tempdb** banco de dados. Você *não pode:*  
  
-   Criar uma tabela temporária global que começa com # #.  
  
-   Executar um backup ou restauração de **tempdb**.  
  
-   Modificar as permissões para **tempdb** com o **GRANT**, **DENY**, ou **REVOGAR** instruções.  
  
-   Executar **DBCC SHRINKLOG** para **tempdb**tempdb.  
  
-   Executar operações DDL em **tempdb**. Há algumas exceções. Para obter detalhes, consulte a seguinte lista de limitações e restrições em tabelas temporárias locais.  
  
Limitações e restrições em tabelas temporárias locais. Você *não pode:*  
  
-   Renomear uma tabela temporária  
  
-   Crie índices não clusterizados, exibições ou partições em uma tabela temporária. **ALTER INDEX** pode ser usado para recriar um índice clusterizado para uma tabela criada com um.  
  
-   Modificar permissões em tabelas temporárias com GRANT, DENY ou REVOKE instruções.  
  
-   Execute comandos do console de banco de dados em tabelas temporárias.  
  
-   Use o mesmo nome para duas ou mais tabelas temporárias dentro do mesmo lote. Se mais de uma tabela temporária local for usada em um lote, cada uma precisará ter um nome exclusivo. Se várias sessões estão executando o mesmo lote e criar a mesma tabela temporária local, o SQL Server PDW acrescenta internamente um sufixo numérico para o nome de tabela temporária local para manter um nome exclusivo para cada tabela temporária local.  
  
> [!NOTE]  
> Você *pode* criar e atualizar estatísticas em uma tabela temporária. **ALTER INDEX** pode ser usado para recriar um índice clusterizado.  
  
## <a name="permissions"></a>Permissões  
Qualquer usuário pode criar objetos temporários no tempdb. Os usuários podem acessar somente seus próprios objetos, a menos que recebam permissões adicionais. É possível revogar a permissão de conexão ao tempdb para impedir um usuário de usar tempdb, mas isto não é recomendado porque algumas operações rotineiras exigem o uso de tempdb.  
  
## <a name="RelatedTasks"></a>Tarefas relacionadas  
  
|Tarefas|Description|  
|---------|---------------|  
|Criar uma tabela no **tempdb**.|Você pode criar uma tabela temporária de usuário com as instruções CREATE TABLE e CREATE TABLE AS SELECT. Para obter mais informações, consulte [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) e [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md).|  
|Exibir uma lista de tabelas existentes em **tempdb**.|`SELECT * FROM tempdb.sys.tables;`|  
|Exibir uma lista de colunas existentes no **tempdb**.|`SELECT * FROM tempdb.sys.columns;`|  
|Exibir uma lista de objetos existentes no **tempdb**.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
