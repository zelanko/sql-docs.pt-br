---
title: Banco de dados tempdb - Parallel Data Warehouse | Microsoft Docs
description: Banco de dados tempdb no Parallel Data Warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1790ae3bc63a379c1bcf143655f10829db60a339
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960014"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>banco de dados tempdb no Parallel Data Warehouse
**tempdb** é um banco de dados de sistema do PDW do SQL Server que armazena as tabelas temporárias locais para bancos de dados do usuário. Tabelas temporárias são geralmente usadas para melhorar o desempenho da consulta. Por exemplo, você pode usar uma tabela temporária para modularizar um script e reutilizar dados computados.  
  
Para obter mais informações sobre bancos de dados do sistema, consulte [bancos de dados do sistema](system-databases.md).  
  
## <a name="Basics"></a>Principais termos e conceitos  
*tabela temporária local*  
Um *tabelas temporárias locais* usa o prefixo # antes do nome da tabela e é uma tabela temporária criada por uma sessão de usuário local. Cada sessão só pode acessar os dados em tabelas temporárias locais para sua própria sessão.  
  
Cada sessão pode exibir os metadados para tabelas temporárias locais em todas as sessões. Por exemplo, todas as sessões podem exibir os metadados para todas as tabelas temporárias locais com o `SELECT * FROM tempdb.sys.tables` consulta.  
  
tabela temporária global  
*Tabelas temporárias globais*, com suporte no SQL Server com o # # sintaxe, não têm suporte nesta versão do SQL Server PDW.  
  
pdwtempdb  
**pdwtempdb** é o banco de dados que armazena as tabelas temporárias locais.  
  
PDW não implementa tabelas temporárias, usando o SQL Server**tempdb** banco de dados. Em vez disso, o PDW armazena-os em um banco de dados chamado pdwtempdb. Este banco de dados existe em cada nó de computação e é invisível para o usuário por meio de interfaces PDW. No Console do administrador, na página de armazenamento, você verá essas contabilizado para em um banco de dados do sistema do PDW chamado **tempdb sql**.  
  
tempdb  
**tempdb** é o banco de dados do tempdb do SQL Server. Ele usa o registro em log mínimo. SQL Server usa o tempdb em nós de computação para armazenar tabelas temporárias que ele precisa durante a execução de operações do SQL Server.  
  
SQL Server PDW descarta tabelas do **tempdb** quando:  
  
-   A instrução DROP TABLE for executada.  
  
-   Uma sessão é desconectada. Somente as tabelas temporárias para a sessão serão descartadas.  
  
-   O dispositivo é desligada.  
  
-   O nó de controle tem um cluster de failover.  
  
## <a name="general-remarks"></a>Comentários gerais  
SQL Server PDW executa as mesmas operações em tabelas temporárias e tabelas permanentes, a menos que explicitamente indicado em contrário. Por exemplo, os dados em tabelas temporárias locais, assim como tabelas permanentes, são distribuídos ou replicados em todos os nós de computação.  
  
## <a name="LimitationsRestrictions"></a>Limitações e restrições  
Limitações e restrições sobre o SQL Server PDW**tempdb** banco de dados. Você *não é possível:*  
  
-   Criar uma tabela temporária global que começa com # #.  
  
-   Execute um backup ou restauração da **tempdb**.  
  
-   Modificar as permissões para **tempdb** com o **GRANT**, **DENY**, ou **REVOGAR** instruções.  
  
-   Execute **DBCC SHRINKLOG** para **tempdb**tempdb.  
  
-   Executar operações de DDL **tempdb**. Há duas exceções a isso. Para obter detalhes, consulte a seguinte lista de limitações e restrições em tabelas temporárias locais.  
  
Limitações e restrições em tabelas temporárias locais. Você *não é possível:*  
  
-   Renomear uma tabela temporária  
  
-   Crie índices não clusterizados, exibições ou partições em uma tabela temporária. **ALTER INDEX** pode ser usado para recriar um índice clusterizado para uma tabela criada com um.  
  
-   Modificar permissões em tabelas temporárias com GRANT, DENY ou REVOGAR as instruções.  
  
-   Execute comandos do console de banco de dados em tabelas temporárias.  
  
-   Use o mesmo nome para duas ou mais tabelas temporárias dentro do mesmo lote. Se mais de uma tabela temporária local for usada em um lote, cada uma precisará ter um nome exclusivo. Se várias sessões estão executando o mesmo lote e criando a mesma tabela temporária local, o SQL Server PDW acrescentará internamente um sufixo numérico ao nome de tabela temporária local para manter um nome exclusivo para cada tabela temporária local.  
  
> [!NOTE]  
> Você *podem* criar e atualizar as estatísticas em uma tabela temporária. **ALTER INDEX** pode ser usado para recriar um índice clusterizado.  
  
## <a name="permissions"></a>Permissões  
Qualquer usuário pode criar objetos temporários no tempdb. Os usuários podem acessar somente seus próprios objetos, a menos que recebam permissões adicionais. É possível revogar a permissão de conexão ao tempdb para impedir um usuário de usar tempdb, mas isto não é recomendado porque algumas operações rotineiras exigem o uso de tempdb.  
  
## <a name="RelatedTasks"></a>Tarefas relacionadas  
  
|Tarefas|Descrição|  
|---------|---------------|  
|Criar uma tabela no **tempdb**.|Você pode criar uma tabela temporária do usuário com as instruções CREATE TABLE e CREATE TABLE AS SELECT. Para obter mais informações, consulte [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) e [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md).|  
|Exibir uma lista de tabelas existentes no **tempdb**.|`SELECT * FROM tempdb.sys.tables;`|  
|Exibir uma lista de colunas existentes no **tempdb**.|`SELECT * FROM tempdb.sys.columns;`|  
|Exibir uma lista de objetos existentes no **tempdb**.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
