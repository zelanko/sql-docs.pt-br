---
title: Construções do Transact-SQL sem suporte no OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e3f8009c-319d-4d7b-8993-828e55ccde11
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ca94f7ef5ed0c6f070424c47aee10c7848a061d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822444"
---
# <a name="transact-sql-constructs-not-supported-by-in-memory-oltp"></a>Construções do Transact-SQL sem suporte pelo OLTP na memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  As tabelas com otimização de memória, procedimentos armazenados compilados de modo nativo e funções definidas pelo usuário não dão suporte à área de superfície completa do [!INCLUDE[tsql](../../includes/tsql-md.md)] que tem suporte em tabelas com base em disco, procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretados e funções definidas pelo usuário. Ao tentar usar um dos recursos sem suporte, o servidor retornará um erro.  
  
 O texto da mensagem de erro aponta o tipo da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] (recurso, operação, opção, por exemplo), bem como o nome do recurso ou palavra-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] . A maioria dos recursos sem suporte retornará o erro 10794, com o texto da mensagem de erro que o recurso não tem suporte. As tabelas a seguir listam os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de erro, bem como a ação corretiva para resolver o erro.  
  
 Para obter mais informações sobre os recursos com suporte em tabelas com otimização de memória e procedimentos armazenados nativamente compilados, consulte:  
  
-   [Problemas de migração para procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  
  
-   [Suporte ao Transact-SQL para OLTP in-memory](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
-   [Recursos do SQL Server sem suporte para OLTP na Memória](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)  
  
-   [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
## <a name="databases-that-use-in-memory-oltp"></a>Bancos de dados que usam OLTP na memória  
 A tabela a seguir lista os recursos do [!INCLUDE[tsql](../../includes/tsql-md.md)] que não têm suporte, além das palavras-chave que podem ser exibidas no texto da mensagem de erro que envolve um banco de dados de OLTP in-memory. A tabela também lista a resolução para o erro.  
  
|Tipo|Nome|Resolução|  
|----------|----------|----------------|  
|Opção|AUTO_CLOSE|A opção de banco de dados AUTO_CLOSE=ON não tem suporte nos bancos de dados que têm um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Opção|ATTACH_REBUILD_LOG|A opção ATTACH_REBUILD_LOG do banco de dados CREATE não tem suporte nos bancos de dados que têm um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Recurso|DATABASE SNAPSHOT|Não há suporte para a criação de instantâneos de banco de dados nos bancos de dados que têm um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Recurso|Replicação usando o sync_method 'database snapshot' ou 'database snapshot character'|A replicação através do sync_method 'database snapshot' ou 'database snapshot character' não tem suporte nos bancos de dados que têm um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Recurso|DBCC CHECKDB<br /><br /> DBCC CHECKTABLE|DBCC CHECKDB ignora as tabelas com otimização de memória no banco de dados.<br /><br /> DBCC CHECKTABLE apresentará falha nas tabelas com otimização de memória.|  
  
## <a name="memory-optimized-tables"></a>Tabelas com otimização de memória  
 A tabela a seguir lista os recursos do [!INCLUDE[tsql](../../includes/tsql-md.md)] que não têm suporte, além das palavras-chave que podem ser exibidas no texto da mensagem de erro que envolve uma tabela com otimização de memória. A tabela também lista a resolução para o erro.  
  
|Tipo|Nome|Resolução|  
|----------|----------|----------------|  
|Recurso|ON|As tabelas com otimização de memória não podem ser colocadas em um grupo de arquivos ou esquema de partição. Remova a cláusula ON da instrução **CREATE TABLE** .<br /><br /> Todas as tabelas com otimização de memória são mapeadas para um grupo de arquivos com otimização de memória.|  
|Tipo de dados|*Nome do tipo de dados*|Não há suporte para o tipo de dados indicado. Substitua o tipo por um dos tipos de dados com suporte. Para obter mais informações, veja [Tipos de dados com suporte no OLTP in-memory](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md).|  
|Recurso|Colunas computadas|**Aplica-se ao:** [!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)] e [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]<br/>As colunas computadas não têm suporte para tabelas com otimização de memória. Remova as colunas computadas da instrução **CREATE TABLE** .<br/><br/>O [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] e o SQL Server a partir do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] dão suporte a colunas computadas em tabelas com otimização de memória e índices.|  
|Recurso|Replicação|Não há suporte para a replicação nas tabelas com otimização de memória.|  
|Recurso|FILESTREAM|O armazenamento FILESTREAM não tem suporte para colunas de tabelas com otimização de memória. Remova a palavra-chave **FILESTREAM** da definição de coluna.|  
|Recurso|SPARSE|As colunas de tabelas com otimização de memória não podem ser definidas como SPARSE. Remova a palavra-chave **SPARSE** da definição de coluna.|  
|Recurso|ROWGUIDCOL|A opção ROWGUIDCOL não tem suporte para colunas de tabelas com otimização de memória. Remova a palavra-chave **ROWGUIDCOL** da definição de coluna.|  
|Recurso|FOREIGN KEY|**Aplica-se ao:** [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] e SQL Server a partir do [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]<br/>Para tabelas com otimização de memória, há suporte para as restrições de FOREIGN KEY apenas em chaves estrangeiras que referenciam chaves primárias de outras tabelas com otimização de memória. Remova a restrição da definição de tabela se a chave estrangeira referenciar uma restrição exclusiva.<br/><br/>No [!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)], não há suporte para as restrições de FOREIGN KEY em tabelas com otimização de memória.|  
|Recurso|índice clusterizado|Especifique um índice não clusterizado. No caso de um índice de chave primária, especifique **PRIMARY KEY NONCLUSTERED**.|  
|Recurso|DDL em transações|As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não podem se criadas nem descartadas no contexto de uma transação de usuário. Não inicie uma transação e garanta que a configuração da sessão IMPLICIT_TRANSACTIONS esteja OFF antes de executar a instrução CREATE ou DROP.|  
|Recurso|gatilhos DDL|As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não poderão ser criadas nem descartadas se houver um gatilho de servidor ou banco de dados para a operação DDL. Remover os gatilhos de servidor e banco de dados em CREATE/DROP TABLE e CREATE/DROP PROCEDURE.|  
|Recurso|EVENT NOTIFICATION|As tabelas com otimização de memória e os procedimentos armazenados compilados de modo nativo não poderão ser criados nem removidos se houver uma notificação de evento de servidor ou de banco de dados para essa operação DDL. Remova as notificações de eventos de servidor e de banco de dados em CREATE TABLE ou DROP TABLE e em CREATE PROCEDURE ou DROP PROCEDURE.|  
|Recurso|FileTable|As tabelas com otimização de memória não podem ser criadas como tabelas de arquivo. Remova o argumento **AS FileTable** da instrução **CREATE TABLE**|  
|Operação|Atualização de colunas de chave primária|As colunas de chave primária nas tabelas com otimização de memória e em tipos de tabela não podem ser atualizadas. Se a chave primária precisar ser atualizada, exclua a linha antiga e insira a nova linha com a chave primária atualizada.|  
|Operação|CREATE INDEX|Os índices nas tabelas com otimização de memória devem ser especificados embutidos com a instrução **CREATE TABLE** , ou com a instrução **ALTER TABLE** .|  
|Operação|CREATE FULLTEXT INDEX|Os índices de texto completo não têm suporte para tabelas com otimização de memória.|  
|Operação|alteração de esquema|Tabelas com otimização de memória e procedimentos armazenados compilados nativamente não dão suporte a algumas alterações de esquema:<br/> [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] e SQL Server a partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]: há suporte para as operações ALTER TABLE, ALTER PROCEDURE e sp_rename. Não há suporte para outras alterações de esquema, por exemplo, adição de propriedades estendidas.<br/><br/>[!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]: há suporte para operações ALTER TABLE e ALTER PROCEDURE. Não há suporte para outras alterações de esquema, incluindo sp_rename.<br/><br/>[!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)]: não há suporte para alterações de esquema. Para alterar a definição de uma tabela com otimização de memória ou um procedimento armazenado compilado nativamente, primeiro remova o objeto e, em seguida, recrie-o com a definição desejada.| 
|Operação|TRUNCATE TABLE|A operação TRUNCATE não tem suporte para tabelas com otimização de memória. Para remover todas as linhas de uma tabela, exclua todas as linhas usando **DELETE FROM***table* ou remova e recrie a tabela.|  
|Operação|ALTER AUTHORIZATION|Não há suporte para alteração do proprietário de uma tabela com otimização de memória ou procedimentos armazenados nativamente compilados existentes. Descarte e recrie a tabela ou o procedimento para alterar a propriedade.|  
|Operação|ALTER SCHEMA|Não há suporte para a transferência de uma tabela ou de um procedimento armazenado compilado nativamente existente para outro esquema. Remova e recrie o objeto para fazer a transferência entre esquemas.|  
|Operação|DBCC CHECKTABLE|Não há suporte para DBCC CHECKTABLE em tabelas com otimização de memória. Para verificar a integridade dos arquivos de ponto de verificação em disco, faça um backup do grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Recurso|ANSI_PADDING OFF|A opção de sessão **ANSI_PADDING** deve estar ON na criação de tabelas com otimização de memória ou procedimentos armazenados compilados de modo nativo. Execute **SET ANSI_PADDING ON** antes de executar a instrução CREATE.|  
|Opção|DATA_COMPRESSION|A compactação de dados não tem suporte para tabelas com otimização de memória. Remova a opção da definição de tabela.|  
|Recurso|DTC|As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não podem ser acessados de transações distribuídas. Em vez disso, use transações SQL.|  
|Operação|Tabelas com otimização de memória como destino de MERGE|As tabelas com otimização de memória não podem ser o destino de uma operação **MERGE** . Em vez disso, use as instruções **INSERT**, **UPDATE** e **DELETE**.|  
  
## <a name="indexes-on-memory-optimized-tables"></a>Índices em tabelas com otimização de memória  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de um erro que envolve um índice em uma tabela com otimização de memória, bem como a ação corretiva para resolver o erro.  
  
|Tipo|Nome|Resolução|  
|----------|----------|----------------|  
|Recurso|Índice filtrado|Os índices filtrados não têm suporte com tabelas com otimização de memória. Omita a cláusula **WHERE** da especificação de índice.|  
|Recurso|Colunas incluídas|Especificar colunas incluídas não é necessário para tabelas com otimização de memória. Todas as colunas da tabela com otimização de memória são incluídas implicitamente em cada índice com otimização de memória.|  
|Operação|DROP INDEX|Não há suporte para o descarte de índices nas tabelas com otimização de memória. Você pode excluir índices usando ALTER TABLE.<br /><br /> Para obter mais informações, veja [Alterando tabelas com otimização de memória](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md).|  
|Opção de índice|*Opção de índice*|Há suporte para apenas uma opção de índice – BUCKET_COUNT para índices de HASH.|  
  
## <a name="nonclustered-hash-indexes"></a>Índices de hash não clusterizados  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de um erro que envolve um índice de hash não clusterizado, bem como a ação corretiva para resolver o erro.  
  
|Tipo|Nome|Resolução|  
|----------|----------|----------------|  
|Opção|ASC/DESC|Os índices de hash não clusterizados não são ordenados. Remova as palavras-chave **ASC** e **DESC** da especificação de chave de índice.|  
  
## <a name="natively-compiled-stored-procedures-and-user-defined-functions"></a>Funções definidas pelo usuário e procedimentos armazenados compilados nativamente  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de um erro que envolve procedimentos armazenados compilados de modo nativo e funções definidas pelo usuário, bem como a ação corretiva para resolver o erro.  
  
|Tipo|Recurso|Resolução|  
|----------|-------------|----------------|  
|Recurso|Variáveis de tabela alinhadas|Os tipos de tabela não podem ser declarados alinhados com declarações de variável. Os tipos de tabela devem ser declarados explicitamente usando uma instrução **CREATE TYPE** .|  
|Recurso|Cursores|Os cursores não têm suporte em procedimentos armazenados nativamente compilados.<br /><br /> Ao executar o procedimento no cliente, use RPC em vez da API do cursor. Com o ODBC, evite a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] de **EXECUTE**, em vez de especificar o nome do procedimento diretamente.<br /><br /> Ao executar o procedimento de um lote do [!INCLUDE[tsql](../../includes/tsql-md.md)] ou outro procedimento armazenado, evite usar um cursor com o procedimento armazenado nativamente compilado.<br /><br /> Ao criar um procedimento armazenado compilado de modo nativo, em vez de usar um cursor, use a lógica baseada em conjunto ou um loop **WHILE** .|  
|Recurso|Padrões de parâmetro não constantes|Ao usar valores padrão com parâmetros em procedimentos armazenados nativamente compilados, os valores devem ser constantes. Remova todos os curingas das declarações de parâmetro.|  
|Recurso|EXTERNAL|Os procedimentos armazenados CLR não podem ser compilados de modo nativo. Remova a cláusula AS EXTERNAL ou a opção NATIVE_COMPILATION da instrução CREATE PROCEDURE.|  
|Recurso|Procedimentos armazenados numerados|Os procedimentos armazenados nativamente compilados não podem ser numerados. Remova o **;***number* da instrução **CREATE PROCEDURE**.|  
|Recurso|INSERT de várias linhas... Instruções VALUES|Não é possível inserir várias linhas que usam a mesma instrução **INSERT** em um procedimento armazenado compilado de modo nativo. Crie instruções **INSERT** para cada linha.|  
|Recurso|CETs (expressões de tabela comum)|As CTEs (expressões de tabela comuns) não têm suporte em procedimentos armazenados nativamente compilados. Regravar a consulta.|  
|Recurso|COMPUTE|Não há suporte para a cláusula **COMPUTE** . Remova-a da consulta.|  
|Recurso|SELECT INTO|Não há suporte para a cláusula **INTO** na instrução **SELECT** . Reescreva a consulta como **INSERT INTO** *Tabela* **SELECT**.|  
|Recurso|lista de colunas de inserção incompleta|Em geral, os valores das instruções INSERT devem ser especificados para todas as colunas na tabela.<br /><br /> No entanto, damos suporte a restrições DEFAULT e colunas IDENTITY(1,1) em tabelas com otimização de memória. Essas colunas podem ser (no caso colunas IDENTITY, devem ser) omitidas da lista de colunas INSERT.|  
|Recurso|*Função*|Algumas funções internas ainda não têm suporte em procedimentos armazenados nativamente compilados. Remova a função rejeitada do procedimento armazenado. Para obter mais informações sobre funções internas com suporte, veja<br />[Recursos com suporte para módulos T-SQL compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)ou<br />[Procedimentos armazenados compilados de modo nativo](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Recurso|CASE|**Aplica-se ao:** [!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)] e SQL Server a partir do [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]<br/>**Não** há suporte para expressões CASE em procedimentos armazenados compilados nativamente. Crie consultas para cada caso. Para obter mais informações,veja [Implementando uma expressão CASE em um procedimento armazenado compilado de modo nativo](../../relational-databases/in-memory-oltp/implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md).<br/><br/>O [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] e o SQL Server a partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] dão suporte a expressões CASE.|  
|Recurso|INSERT EXECUTE|Remova a referência.|  
|Recurso|Execute|Com suporte somente para executar funções definidas pelo usuário e procedimentos armazenados compilados nativamente.|  
|Recurso|agregações definidas pelo usuário|As funções de agregação definidas pelo usuário não podem ser usadas em procedimentos armazenados nativamente compilados. Remova a referência à função do procedimento.|  
|Recurso|metadados do modo de procura|Os procedimentos armazenados nativamente compilados não oferecem suporte aos metadados do modo de procura. Verifique se a opção de sessão **NO_BROWSETABLE** está definida como OFF.|  
|Recurso|DELETE com a cláusula FROM|Não há suporte para a cláusula **FROM** em instruções **DELETE** com uma fonte de tabela em procedimentos armazenados compilados de modo nativo.<br /><br /> **DELETE** com a cláusula **FROM** tem suporte quando ela é usada para indicar a tabela do local em que haverá exclusão.|  
|Recurso|UPDATE com a cláusula FROM|Não há suporte para a cláusula **FROM** em instruções **UPDATE** em procedimentos armazenados compilados de modo nativo.| 
|Recurso|procedimentos temporários|Os procedimentos armazenados temporários não podem ser compilados nativamente. Crie um procedimento armazenado nativamente compilado permanente ou um procedimento armazenado do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado temporário.|  
|Nível de isolamento|READ UNCOMMITTED|O nível de isolamento READ UNCOMMITTED não tem suporte para procedimentos armazenados nativamente compilados. Use um nível de isolamento com suporte, como SNAPSHOT.|  
|Nível de isolamento|READ COMMITTED|O nível de isolamento READ COMMITTED não tem suporte para procedimentos armazenados nativamente compilados. Use um nível de isolamento com suporte, como SNAPSHOT.|  
|Recurso|tabelas temporárias|As tabelas em tempdb não podem ser usadas em procedimentos armazenados nativamente compilados. Em vez disso, use uma variável de tabela ou uma tabela com otimização de memória com DURABILITY=SCHEMA_ONLY.|  
|Recurso|DTC|As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não podem ser acessados de transações distribuídas. Em vez disso, use transações SQL.|  
|Recurso|EXECUTE WITH RECOMPILE|Não há suporte para a opção **WITH RECOMPILE** em procedimentos armazenados compilados de modo nativo.|  
|Recurso|Execução da conexão de administrador dedicada.|Os procedimentos armazenados nativamente compilados não podem ser executados da DAC (conexão do administrador dedicado). Use uma conexão normal.|  
|Operação|ponto de salvamento|Os procedimentos armazenados nativamente compilados não podem ser invocados de transações que tenham um ponto de salvamento ativo. Remova o ponto de salvamento da transação.|  
|Operação|ALTER AUTHORIZATION|Não há suporte para alteração do proprietário de uma tabela com otimização de memória ou procedimentos armazenados nativamente compilados existentes. Descarte e recrie a tabela ou o procedimento para alterar a propriedade.|  
|Operador|OPENROWSET|Não há suporte para esse operador. Remova **OPENROWSET** do procedimento armazenado compilado de modo nativo.|  
|Operador|OPENQUERY|Não há suporte para esse operador. Remova **OPENQUERY** do procedimento armazenado compilado de modo nativo.|  
|Operador|OPENDATASOURCE|Não há suporte para esse operador. Remova **OPENDATASOURCE** do procedimento armazenado compilado de modo nativo.|  
|Operador|OPENXML|Não há suporte para esse operador. Remova **OPENXML** do procedimento armazenado compilado de modo nativo.|  
|Operador|CONTAINSTABLE|Não há suporte para esse operador. Remova **CONTAINSTABLE** do procedimento armazenado compilado de modo nativo.|  
|Operador|FREETEXTTABLE|Não há suporte para esse operador. Remova **FREETEXTTABLE** do procedimento armazenado compilado de modo nativo.|  
|Recurso|funções com valor de tabela|As funções com valor de tabela não podem ser referenciadas de procedimentos armazenados nativamente compilados. Uma solução possível para essa restrição é adicionar a lógica das funções com valor de tabela ao corpo do procedimento.|  
|Operador|CHANGETABLE|Não há suporte para esse operador. Remova **CHANGETABLE** do procedimento armazenado compilado de modo nativo.|  
|Operador|GOTO|Não há suporte para esse operador. Use outras construções de procedimento, como WHILE.|  
|Operador|OFFSET|Não há suporte para esse operador. Remova **OFFSET** do procedimento armazenado compilado de modo nativo.|  
|Operador|INTERSECT|Não há suporte para esse operador. Remova **INTERSECT** do procedimento armazenado compilado de modo nativo. Em alguns casos, um INNER JOIN pode ser usado para obter o mesmo resultado.|  
|Operador|EXCEPT|Não há suporte para esse operador. Remova **EXCEPT** do procedimento armazenado compilado de modo nativo.|  
|Operador|APPLY|**Aplica-se ao:** [!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)] e SQL Server a partir do [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]<br/>Não há suporte para esse operador. Remova **APPLY** do procedimento armazenado compilado de modo nativo.<br/><br/>O [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] e o SQL Server a partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] dão suporte ao operador APPLY em módulos compilados nativamente.|  
|Operador|PIVOT|Não há suporte para esse operador. Remova **PIVOT** do procedimento armazenado compilado de modo nativo.|  
|Operador|UNPIVOT|Não há suporte para esse operador. Remova **UNPIVOT** do procedimento armazenado compilado de modo nativo.|  
|Operador|CONTAINS|Não há suporte para esse operador. Remova **CONTAINS** do procedimento armazenado compilado de modo nativo.|  
|Operador|FREETEXT|Não há suporte para esse operador. Remova **FREETEXT** do procedimento armazenado compilado de modo nativo.|  
|Operador|TSEQUAL|Não há suporte para esse operador. Remova **TSEQUAL** do procedimento armazenado compilado de modo nativo.|  
|Operador|LIKE|Não há suporte para esse operador. Remova **LIKE** do procedimento armazenado compilado de modo nativo.|  
|Operador|NEXT VALUE FOR|As sequências não podem referenciadas dentro de procedimentos armazenados nativamente compilados. Obtenha o valor usando [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado e transmita-o ao procedimento armazenado nativamente compilado. Para obter mais informações, veja [Implementando IDENTITY em uma tabela com otimização de memória](../../relational-databases/in-memory-oltp/implementing-identity-in-a-memory-optimized-table.md).|  
|Opção Set|*opção*|As opções SET não podem ser alteradas dentro de procedimentos armazenados nativamente compilados. Algumas opções podem ser definidas com a instrução BEGIN ATOMIC. Para obter mais informações, confira a seção sobre blocos atômicos em [Procedimentos armazenados compilados de modo nativo](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Operando|TABLESAMPLE|Não há suporte para esse operador. Remova **TABLESAMPLE** do procedimento armazenado compilado de modo nativo.|  
|Opção|RECOMPILE|Os procedimentos armazenados nativamente compilados são compilados no tempo de criação. Remova **RECOMPILE** da definição de procedimento.<br /><br /> Você pode executar sp_recompile em um procedimento armazenado compilado nativamente, o que faz com que ele recompile na próxima execução.|  
|Opção|ENCRYPTION|Não há suporte para essa opção. Remova **ENCRYPTION** da definição do procedimento.|  
|Opção|FOR REPLICATION|Os procedimentos armazenados nativamente compilados não podem ser criados para replicação. Remova **FOR REPLICATION** da definição do procedimento.|  
|Opção|FOR XML|Não há suporte para essa opção. Remova **FOR XML** do procedimento armazenado compilado de modo nativo.|  
|Opção|FOR BROWSE|Não há suporte para essa opção. Remova **FOR BROWSE** do procedimento armazenado compilado de modo nativo.|  
|Dica de junção|HASH, MERGE|Os procedimentos armazenados nativamente compilados oferecem suporte somente a junções de loops aninhados. Não há suporte para junções de hash e mesclagem. Remova a dica de junção.|  
|Dica de consulta|*Dica de consulta*|Essa dica de consulta não está dentro de procedimentos armazenados nativamente compilados. Para obter dicas de consulta com suporte, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).|  
|Opção|PERCENT|Essa opção não tem suporte com cláusulas **TOP** . Remova **PERCENT** da consulta no procedimento armazenado compilado de modo nativo.|  
|Opção|WITH TIES|**Aplica-se ao:** [!INCLUDE[ssSDS14_md](../../includes/sssql14-md.md)] e [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]<br/>Essa opção não tem suporte com cláusulas **TOP** . Remova **WITH TIES** da consulta no procedimento armazenado compilado de modo nativo.<br/><br/>O [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] e o SQL Server a partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] dão suporte a opção **TOP WITH TIES**.|  
|Função de agregação|*Função de agregação*|Não há suporte para todas as funções de agregação. Para obter mais informações sobre as funções de agregação com suporte em módulos T-SQL compilados nativamente, consulte [Recursos com suporte em módulos T-SQL compilados nativamente](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).|  
|Função de classificação|*Função de classificação*|As funções de classificação não têm suporte em procedimentos armazenados nativamente compilados. Remova-as da definição de procedimento.|  
|Função|*Função*|Não há suporte para essa função. Para obter mais informações sobre as funções com suporte em módulos T-SQL compilados nativamente, consulte [Recursos com suporte em módulos T-SQL compilados nativamente](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).|  
|de|*Instrução*|Não há suporte para essa instrução. Para obter mais informações sobre as funções com suporte em módulos T-SQL compilados nativamente, consulte [Recursos com suporte em módulos T-SQL compilados nativamente](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).|  
|Recurso|MIN e MAX usados com cadeias de caracteres e binários|As funções de agregação **MIN** e **MAX** não podem ser usadas para valores de cadeias de caracteres binários e caracteres dentro de procedimentos armazenados compilados de modo nativo.|  
|Recurso|GROUP BY ALL|ALL não pode ser usado com cláusulas GROUP BY em procedimentos armazenados compilados de modo nativo. Remova ALL da cláusula GROUP BY.|  
|Recurso|GROUP BY ()|Não suporte para o agrupamento por uma lista vazia. Remova a cláusula GROUP BY ou inclua colunas na lista de agrupamentos.|  
|Recurso|ROLLUP|**ROLLUP** não pode ser usado com cláusulas **GROUP BY** em procedimentos armazenados compilados de modo nativo. Remova **ROLLUP** da definição de procedimento.|  
|Recurso|CUBE|**CUBE** não pode ser usado com cláusulas **GROUP BY** em procedimentos armazenados compilados de modo nativo. Remova **CUBE** da definição de procedimento.|  
|Recurso|GROUPING SETS|**GROUPING SETS** não pode ser usado com cláusulas **GROUP BY** em procedimentos armazenados compilados de modo nativo. Remova **GROUPING SETS** da definição do procedimento.|  
|Recurso|BEGIN TRANSACTION, COMMIT TRANSACTION e ROLLBACK TRANSACTION|Use blocos ATOMIC para controlar transações e tratamento de erros. Para obter mais informações, veja [Blocos atômicos](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).|  
|Recurso|Declarações de variável de tabela embutidas.|As variáveis de tabela devem referenciar explicitamente os tipos de tabela com otimização de memória definidos. Você deve criar um tipo de tabela com otimização de memória e usar esse tipo para a declaração variável, em vez de especificar o tipo embutido.|  
|Recurso|Tabelas baseadas em disco|As tabelas baseadas em disco não podem ser acessadas nos procedimentos armazenados compilados de modo nativo. Remova as referências a tabelas baseadas em disco dos procedimentos armazenados compilados de modo nativo. Ou migre as tabelas baseadas em disco para tabelas com otimização de memória.|  
|Recurso|exibições|As exibições não podem ser acessadas nos procedimentos armazenados compilados de modo nativo. Em vez das exibições, referencie as tabelas base subjacentes.|  
|Recurso|Funções com valor de tabela|**Aplica-se ao:** [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] e SQL Server a partir do [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]<br/>Funções com valor de tabela com várias instruções não podem ser acessadas em módulos T-SQL compilados nativamente. Há suporte para funções com valor de tabela embutidas, mas elas devem ser criadas WITH NATIVE_COMPILATION.<br/><br/>**Aplica-se ao**: [!INCLUDE[ssSQL14-md](../../includes/ssSQL14-md.md)]<br/>As funções com valor de tabela não podem ser referenciadas em módulos T-SQL compilados nativamente.|  
|Opção|PRINT|Remover referência|  
|Recurso|DDL|Não há suporte para DDL em módulos T-SQL compilados nativamente.|  
|Opção|STATISTICS XML|Sem suporte. Quando você executa uma consulta com STATISTICS XML habilitado, o conteúdo XML é retornado sem a parte do procedimento armazenado compilado nativamente.|  
  
## <a name="transactions-that-access-memory-optimized-tables"></a>Transações que acessam tabelas com otimização de memória  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de um erro que envolve transações que acessam tabelas com otimização de memória, bem como a ação corretiva para resolver o erro.  
  
|Tipo|Nome|Resolução|  
|----------|----------|----------------|  
|Recurso|ponto de salvamento|Não há suporte para a criação de pontos de salvamento explícitos em transações que acessam tabelas com otimização de memória.|  
|Recurso|transação associada|As sessões associadas não podem participar de transações que acessam tabelas com otimização de memória. Não associe a sessão antes de executar o procedimento.|  
|Recurso|DTC|As transações que acessam tabelas com otimização de memória não podem ser transações distribuídas.|  
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
