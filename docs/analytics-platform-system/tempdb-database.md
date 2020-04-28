---
title: Banco de dados tempdb
description: Banco de dados tempdb em paralelo data warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3772e2b4cabac84c00854eba85f7a0c2a33d48bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400146"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>banco de dados tempdb em paralelo data warehouse
**tempdb** é um banco de dados do sistema SQL Server PDW que armazena tabelas temporárias locais para bancos de dados de usuário. As tabelas temporárias são geralmente usadas para melhorar o desempenho da consulta. Por exemplo, você pode usar uma tabela temporária para modularizar um script e reutilizar dados computados.  
  
Para obter mais informações sobre bancos de dados do sistema, consulte [bancos de dados do sistema](system-databases.md).  
  
## <a name="key-terms-and-concepts"></a><a name="Basics"></a>Principais termos e conceitos  
*tabela temporária local*  
Uma *tabela temporária local* usa o prefixo # antes do nome da tabela e é uma tabela temporária criada por uma sessão de usuário local. Cada sessão só pode acessar os dados em tabelas temporárias locais para sua própria sessão.  
  
Cada sessão pode exibir os metadados para tabelas temporárias locais em todas as sessões. Por exemplo, todas as sessões podem exibir os metadados de todas as tabelas temporárias `SELECT * FROM tempdb.sys.tables` locais com a consulta.  
  
tabela temporária global  
As *tabelas temporárias globais*, com suporte na SQL Server com a sintaxe # #, não têm suporte nesta versão do SQL Server PDW.  
  
pdwtempdb  
**pdwtempdb** é o banco de dados que armazena tabelas temporárias locais.  
  
O PDW não implementa tabelas temporárias usando o banco de dados SQL Server**tempdb** . Em vez disso, o PDW as armazena em um banco de dados chamado pdwtempdb. Esse banco de dados existe em cada nó de computação e é invisível para o usuário por meio das interfaces do PDW. No console de administração, na página armazenamento, você verá isso em um banco de dados do sistema PDW chamado **tempdb-SQL**.  
  
tempdb  
**tempdb** é o banco de dados SQL Server tempdb. Ele usa o registro em log mínimo. O SQL Server usa tempdb nos nós de computação para armazenar tabelas temporárias necessárias no decorrer da realização de operações de SQL Server.  
  
SQL Server PDW descarta as tabelas do **tempdb** quando:  
  
-   A instrução DROP TABLE é executada.  
  
-   Uma sessão está desconectada. Somente tabelas temporárias para a sessão são descartadas.  
  
-   O dispositivo está desligado.  
  
-   O nó de controle tem um failover de cluster.  
  
## <a name="general-remarks"></a>Comentários gerais  
SQL Server PDW executa as mesmas operações em tabelas temporárias e tabelas permanentes, a menos que explicitamente declarado de outra forma. Por exemplo, os dados em tabelas temporárias locais, assim como as tabelas permanentes, são distribuídos ou replicados em todos os nós de computação.  
  
## <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a>Limitações e restrições  
Limitações e restrições no banco de dados SQL Server PDW**tempdb** . Você *não pode:*  
  
-   Crie uma tabela temporária global que comece com # #.  
  
-   Execute um backup ou uma restauração de **tempdb**.  
  
-   Modifique as permissões para **tempdb** com as instruções **Grant**, **Deny**ou **REVOKE** .  
  
-   Execute **DBCC SHRINKLOG** para **tempdb**tempdb.  
  
-   Execute operações DDL em **tempdb**. Há algumas exceções a isso. Para obter detalhes, consulte a lista de limitações e restrições em tabelas temporárias locais a seguir.  
  
Limitações e restrições em tabelas temporárias locais. Você *não pode:*  
  
-   Renomear uma tabela temporária  
  
-   Crie partições, exibições ou índices não clusterizados em uma tabela temporária. **ALTER INDEX** pode ser usado para recriar um índice clusterizado para uma tabela criada com um.  
  
-   Modifique as permissões para tabelas temporárias com as instruções GRANT, DENY ou REVOKE.  
  
-   Execute comandos do console do banco de dados em tabelas temporárias.  
  
-   Use o mesmo nome para duas ou mais tabelas temporárias dentro do mesmo lote. Se mais de uma tabela temporária local for usada em um lote, cada uma precisará ter um nome exclusivo. Se várias sessões estiverem executando o mesmo lote e criando a mesma tabela temporária local, o SQL Server PDW acrescentará internamente um sufixo numérico ao nome da tabela temporária local para manter um nome exclusivo para cada tabela temporária local.  
  
> [!NOTE]  
> Você *pode* criar e atualizar estatísticas em uma tabela temporária. **ALTER INDEX** pode ser usado para recriar um índice clusterizado.  
  
## <a name="permissions"></a>Permissões  
Qualquer usuário pode criar objetos temporários no tempdb. Os usuários podem acessar somente seus próprios objetos, a menos que recebam permissões adicionais. É possível revogar a permissão de conexão ao tempdb para impedir um usuário de usar tempdb, mas isto não é recomendado porque algumas operações rotineiras exigem o uso de tempdb.  
  
## <a name="related-tasks"></a><a name="RelatedTasks"></a>Related Tasks  
  
|Tarefas|Descrição|  
|---------|---------------|  
|Crie uma tabela em **tempdb**.|Você pode criar uma tabela temporária de usuário com as instruções CREATE TABLE e CREATE TABLE como SELECT. Para obter mais informações, consulte [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) e [CREATE TABLE como SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md).|  
|Exiba uma lista de tabelas existentes no **tempdb**.|`SELECT * FROM tempdb.sys.tables;`|  
|Exiba uma lista de colunas existentes em **tempdb**.|`SELECT * FROM tempdb.sys.columns;`|  
|Exiba uma lista de objetos existentes no **tempdb**.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
