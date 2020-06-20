---
title: Construções do Transact-SQL sem suporte no OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e3f8009c-319d-4d7b-8993-828e55ccde11
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b5df47d05730b8f6ec6a82045686d462ace1682
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025557"
---
# <a name="transact-sql-constructs-not-supported-by-in-memory-oltp"></a>Construções do Transact-SQL sem suporte pelo OLTP na memória
  As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não oferecem suporte à área de superfície completa do [!INCLUDE[tsql](../../includes/tsql-md.md)] que tem suporte em tabelas com base em disco e procedimentos armazenados pelo [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado. Ao tentar usar um dos recursos sem suporte, o servidor retornará um erro.  
  
 O texto da mensagem de erro aponta o tipo da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] (recurso, operação, opção, por exemplo), bem como o nome do recurso ou palavra-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] . A maioria dos recursos sem suporte retornará o erro 10794, com o texto da mensagem de erro que o recurso não tem suporte. As tabelas a seguir listam os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de erro, bem como a ação corretiva para resolver o erro.  
  
 Para obter mais informações sobre os recursos com suporte em tabelas com otimização de memória e procedimentos armazenados nativamente compilados, consulte:  
  
-   [Problemas de migração para procedimentos armazenados compilados nativamente](migration-issues-for-natively-compiled-stored-procedures.md)  
  
-   [Suporte ao Transact-SQL para OLTP in-memory](transact-sql-support-for-in-memory-oltp.md)  
  
-   [Recursos do SQL Server com suporte](unsupported-sql-server-features-for-in-memory-oltp.md)  
  
-   [Procedimentos armazenados compilados nativamente](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
## <a name="databases-that-use-in-memory-oltp"></a>Bancos de dados que usam OLTP na memória  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem ser exibidos no texto da mensagem de erro que envolve um banco de dados de OLTP na memória.  
  
|Type|Nome|Resolução|  
|----------|----------|----------------|  
|Opção|AUTO_CLOSE|A opção de banco de dados AUTO_CLOSE=ON não tem suporte nos bancos de dados que têm um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Opção|ATTACH_REBUILD_LOG|A opção ATTACH_REBUILD_LOG do banco de dados CREATE não tem suporte nos bancos de dados que têm um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Recurso|DATABASE SNAPSHOT|Não há suporte para a criação de instantâneos de banco de dados nos bancos de dados que têm um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Recurso|Replicação usando o sync_method 'database snapshot' ou 'database snapshot character'|A replicação através do sync_method 'database snapshot' ou 'database snapshot character' não tem suporte nos bancos de dados que têm um grupo de arquivos MEMORY_OPTIMIZED_DATA.|  
|Recurso|DBCC CHECKDB<br /><br /> DBCC CHECKTABLE|DBCC CHECKDB ignora as tabelas com otimização de memória no banco de dados.<br /><br /> DBCC CHECKTABLE apresentará falha nas tabelas com otimização de memória.|  
  
## <a name="memory-optimized-tables"></a>Tabelas com otimização de memória  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de um erro que envolve uma tabela com otimização de memória, bem como a ação corretiva para resolver o erro.  
  
|Type|Nome|Resolução|  
|----------|----------|----------------|  
|Recurso|ATIVADO|As tabelas com otimização de memória não podem ser colocadas em um grupo de arquivos ou esquema de partição. Remova a cláusula ON da instrução `CREATE TABLE`.|  
|Tipo de dados|*Nome do tipo de dados*|Não há suporte para o tipo de dados indicado. Substitua o tipo por um dos tipos de dados com suporte. Para obter mais informações, consulte [tipos de dados com suporte](supported-data-types-for-in-memory-oltp.md).|  
|Recurso|Colunas computadas|As colunas computadas não têm suporte para tabelas com otimização de memória. Remova as colunas computadas da instrução `CREATE TABLE`.|  
|Recurso|Replicação|Não há suporte para a replicação nas tabelas com otimização de memória.|  
|Recurso|FILESTREAM|O armazenamento FILESTREAM não tem suporte para colunas de tabelas com otimização de memória. Remova a palavra-chave `FILESTREAM` da definição de coluna.|  
|Recurso|SPARSE|As colunas de tabelas com otimização de memória não podem ser definidas como SPARSE. Remova a palavra-chave `SPARSE` da definição de coluna.|  
|Recurso|ROWGUIDCOL|A opção ROWGUIDCOL não tem suporte para colunas de tabelas com otimização de memória. Remova a palavra-chave `ROWGUIDCOL` da definição de coluna.|  
|Recurso|FOREIGN KEY|As restrições FOREIGN KEY não têm suporte para tabelas com otimização de memória. Remova a restrição da definição de tabela.<br /><br /> Para obter informações sobre como mitigar a falta de suporte para restrições, consulte [migrando restrições CHECK e Foreign Key](../../database-engine/migrating-check-and-foreign-key-constraints.md).|  
|Recurso|CHECK|As restrições CHECK não têm suporte para tabelas com otimização de memória. Remova a restrição da definição de tabela.<br /><br /> Para obter informações sobre como mitigar a falta de suporte para restrições, consulte [migrando restrições CHECK e Foreign Key](../../database-engine/migrating-check-and-foreign-key-constraints.md).|  
|Recurso|UNIQUE|As restrições UNIQUE não têm suporte nas tabelas com otimização de memória. Remova a restrição da definição de tabela.<br /><br /> Para obter informações sobre como mitigar a falta de suporte para restrições, consulte [migrando restrições CHECK e Foreign Key](../../database-engine/migrating-check-and-foreign-key-constraints.md).|  
|Recurso|COLUMNSTORE|Os índices COLUMNSTORE não têm suporte com tabelas com otimização de memória. Em vez disso, especifique um índice NONCLUSTERED ou NONCLUSTERED HASH.|  
|Recurso|índice clusterizado|Especifique um índice não clusterizado. No caso de um índice de chave primária, não deixe de especificar `PRIMARY KEY NONCLUSTERED [HASH]`.|  
|Recurso|página de código diferente de 1252|As colunas em tabelas com otimização de memória com tipos de dados `char` e `varchar` devem usar a página de código 1252. Use n(var)char em vez de (var)char ou use uma ordenação com página de código 1252 (por exemplo, Latin1_General_BIN2). Para obter mais informações, consulte [Páginas de código de ordenações](../../database-engine/collations-and-code-pages.md).|  
|Recurso|DDL em transações|As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não podem se criadas nem descartadas no contexto de uma transação de usuário. Não inicie uma transação e garanta que a configuração da sessão IMPLICIT_TRANSACTIONS esteja OFF antes de executar a instrução CREATE ou DROP.|  
|Recurso|gatilhos DDL|As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não poderão ser criadas nem descartadas se houver um gatilho de servidor ou banco de dados para a operação DDL. Remover os gatilhos de servidor e banco de dados em CREATE/DROP TABLE e CREATE/DROP PROCEDURE.|  
|Recurso|EVENT NOTIFICATION|As tabelas com otimização de memória e os procedimentos armazenados compilados de modo nativo não poderão ser criados nem removidos se houver uma notificação de evento de servidor ou de banco de dados para essa operação DDL. Remova as notificações de eventos de servidor e de banco de dados em CREATE TABLE ou DROP TABLE e em CREATE PROCEDURE ou DROP PROCEDURE.|  
|Recurso|FileTable|As tabelas com otimização de memória não podem ser criadas como tabelas de arquivo. Remova o argumento `AS FileTable` da instrução `CREATE TABLE`|  
|Operação|Atualização de colunas de chave primária|As colunas de chave primária nas tabelas com otimização de memória e em tipos de tabela não podem ser atualizadas. Se a chave primária precisar ser atualizada, exclua a linha antiga e insira a nova linha com a chave primária atualizada.|  
|Operação|CREATE INDEX|Os índices nas tabelas com otimização de memória devem ser especificados em linha com a instrução `CREATE TABLE`. Para adicionar um índice a uma tabela com otimização de memória, descarte e recrie a tabela, incluindo a especificação do novo índice.|  
|Operação|ALTER TABLE|Não há suporte para a alteração das tabelas com otimização de memória. Descarte e recrie a tabela usando a definição da tabela atualizada.|  
|Operação|CREATE FULLTEXT INDEX|Os índices de texto completo não têm suporte para tabelas com otimização de memória.|  
|Operação|alteração de esquema|As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não oferecem suporte a alterações de esquema, por exemplo, `sp_rename`.<br /><br /> A tentativa de fazer alterações de esquema, como renomear uma tabela, gerará o erro 12320. As operações que exigem alteração na versão do esquema, por exemplo, renomeação, não têm suporte nas tabelas com otimização de memória.<br /><br /> Para alterar o esquema, descarte e recrie a tabela ou o procedimento usando uma definição atualizada.|  
|Operação|CREATE TRIGGER|Não há suporte para gatilhos em tabelas com otimização de memória.|  
|Operação|TRUNCATE TABLE|A operação TRUNCATE não tem suporte para tabelas com otimização de memória. Para remover todas as linhas de uma tabela, exclua todas as linhas usando `DELETE FROM` *Table* ou drop e recrie a tabela.|  
|Operação|ALTER AUTHORIZATION|Não há suporte para alteração do proprietário de uma tabela com otimização de memória ou procedimentos armazenados nativamente compilados existentes. Descarte e recrie a tabela ou o procedimento para alterar a propriedade.|  
|Operação|ALTER SCHEMA|Não há suporte para a alteração do esquema de uma tabela com otimização de memória ou de um procedimento armazenado compilado de modo nativo existente. Remova e recrie a tabela ou o procedimento para alterar o esquema.|  
|Operação|DBCC CHECKTABLE|Não há suporte para DBCC CHECKTABLE nas tabelas com otimização de memória.|  
|Recurso|ANSI_PADDING OFF|A opção de sessão `ANSI_PADDING` deve estar ON na criação de tabelas com otimização de memória ou procedimentos armazenados nativamente compilados. Execute `SET ANSI_PADDING ON` antes de executar a instrução CREATE.|  
|Opção|DATA_COMPRESSION|A compactação de dados não tem suporte para tabelas com otimização de memória. Remova a opção da definição de tabela.|  
|Recurso|DTC|As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não podem ser acessados de transações distribuídas. Em vez disso, use transações SQL.|  
|Recurso|MARS (Vários Conjuntos de Resultados Ativos)|O MARS (Vários Conjuntos de Resultados Ativos) não tem suporte com tabelas com otimização de memória. Esse erro também pode indicar uso de servidor vinculado. O servidor vinculado pode usar MARS. Os servidores vinculados não têm suporte com tabelas com otimização de memória. Conecte-se diretamente ao servidor e ao banco de dados que hospeda as tabelas com otimização de memória.|  
|Operação|Tabelas com otimização de memória como destino de MERGE|As tabelas com otimização de memória não podem ser o destino de uma operação `MERGE`. Use as instruções `INSERT`, `UPDATE` ou `DELETE`.|  
  
## <a name="indexes-on-memory-optimized-tables"></a>Índices em tabelas com otimização de memória  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de um erro que envolve um índice em uma tabela com otimização de memória, bem como a ação corretiva para resolver o erro.  
  
|Type|Nome|Resolução|  
|----------|----------|----------------|  
|Recurso|Índice filtrado|Os índices filtrados não têm suporte com tabelas com otimização de memória. Omita a cláusula `WHERE` da especificação de índice.|  
|Recurso|UNIQUE|Não há suporte para índices exclusivos nas tabelas com otimização de memória. Remova o argumento `UNIQUE` da especificação de índice.|  
|Recurso|Colunas que permitem valor nulo|Todas as colunas na chave de um índice em uma tabela com otimização de memória devem ser especificadas como `NOT NULL`. Inclua a restrição `NOT NULL` com todas as colunas nas chaves de índice.|  
|Recurso|ordenação non-bin2|Todas as colunas de caractere na chave de um índice com otimização de memória devem ser declaradas usando uma ordenação BIN2. Use a cláusula `COLLATE` para definir a ordenação na definição de coluna. Para obter mais informações, consulte [Páginas de código de ordenações](../../database-engine/collations-and-code-pages.md).|  
|Recurso|Colunas incluídas|Especificar colunas incluídas não é necessário para tabelas com otimização de memória. Todas as colunas da tabela com otimização de memória são incluídas implicitamente em cada índice com otimização de memória.|  
|Operação|ALTER INDEX|Não há suporte para a alteração de índices nas tabelas com otimização de memória. Desse modo, descarte a tabela e recrie-a usando a especificação de índice atualizada.|  
|Operação|DROP INDEX|Não há suporte para o descarte de índices nas tabelas com otimização de memória. Descarte a tabela e recrie-a com os índices desejados.|  
|Opção de índice|*Opção de índice*|A opção de índice indicada não tem suporte com índices em tabelas com otimização de memória. Remova a opção da especificação de índice.|  
  
## <a name="nonclustered-hash-indexes"></a>Índices de hash não clusterizados  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de um erro que envolve um índice de hash não clusterizado, bem como a ação corretiva para resolver o erro.  
  
|Type|Nome|Resolução|  
|----------|----------|----------------|  
|Opção|ASC/DESC|Os índices de hash não clusterizados não são ordenados. Remova as palavras-chave `ASC` e `DESC` da especificação de chave de índice.|  
  
## <a name="natively-compiled-stored-procedures"></a>procedimentos armazenados compilados nativamente  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de um erro que envolve procedimentos armazenados nativamente compilados, bem como a ação corretiva para resolver o erro.  
  
|Type|Recurso|Resolução|  
|----------|-------------|----------------|  
|Recurso|Variáveis de tabela alinhadas|Os tipos de tabela não podem ser declarados alinhados com declarações de variável. Os tipos de tabela devem ser declarados explicitamente usando uma instrução `CREATE TYPE`.|  
|Recurso|Cursores|Os cursores não têm suporte em procedimentos armazenados nativamente compilados.<br /><br /> -Ao executar o procedimento do cliente, use RPC em vez da API do cursor. Com o ODBC, evite a instrução `EXECUTE` do [!INCLUDE[tsql](../../includes/tsql-md.md)], em vez de especificar o nome do procedimento diretamente.<br /><br /> -Ao executar o procedimento de um [!INCLUDE[tsql](../../includes/tsql-md.md)] lote ou outro procedimento armazenado, evite usar um cursor com o procedimento armazenado compilado nativamente.<br /><br /> -Ao criar um procedimento armazenado compilado nativamente, em vez de usar um cursor, use a lógica baseada em conjunto ou um `WHILE` loop.|  
|Recurso|Padrões de parâmetro não constantes|Ao usar valores padrão com parâmetros em procedimentos armazenados nativamente compilados, os valores devem ser constantes. Remova todos os curingas das declarações de parâmetro.|  
|Recurso|EXTERNAL|Os procedimentos armazenados CLR não podem ser compilados de modo nativo. Remova a cláusula AS EXTERNAL ou a opção NATIVE_COMPILATION da instrução CREATE PROCEDURE.|  
|Recurso|Procedimentos armazenados numerados|Os procedimentos armazenados nativamente compilados não podem ser numerados. Remova o `;` *número* da `CREATE PROCEDURE` instrução.|  
|Recurso|INSERÇÃO de várias linhas... Instruções VALUEs|Não é possível inserir várias linhas que usam a mesma instrução `INSERT` em um procedimento armazenado nativamente compilado. Crie instruções `INSERT` para cada linha.|  
|Recurso|CETs (expressões de tabela comum)|As CTEs (expressões de tabela comuns) não têm suporte em procedimentos armazenados nativamente compilados. Regravar a consulta.|  
|Recurso|subconsulta|Não há suporte para subconsultas (consultas aninhadas dentro de outra consulta). Regravar a consulta.|  
|Recurso|COMPUTE|Não há suporte para a cláusula `COMPUTE`. Remova-a da consulta.|  
|Recurso|SELECT INTO|A cláusula `INTO` não tem suporte com a instrução `SELECT`. Reescreva a consulta como `INSERT INTO` *tabela* `SELECT` .|  
|Recurso|OUTPUT|Não há suporte para a cláusula `OUTPUT`. Remova-a da consulta.|  
|Recurso|lista de colunas de inserção incompleta|Em instruções `INSERT`, os valores devem ser especificados para todas as colunas na tabela.|  
|Função|*Função*|A função interna não tem suporte em procedimentos armazenados nativamente compilados. Remova a função do procedimento armazenado. Para obter mais informações sobre funções internas com suporte, consulte [procedimentos armazenados compilados nativamente](../in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Recurso|CASE|A instrução `CASE` não tem suporte em consultas dentro de procedimentos armazenados nativamente compilados. Crie consultas para cada caso. Para obter mais informações, consulte [implementando uma instrução Case](implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md).|  
|Recurso|funções definidas pelo usuário|As funções definidas pelo usuário não podem ser usadas em procedimentos armazenados nativamente compilados. Remova a referência à função da definição de procedimento.|  
|Recurso|agregações definidas pelo usuário|As funções de agregação definidas pelo usuário não podem ser usadas em procedimentos armazenados nativamente compilados. Remova a referência à função do procedimento.|  
|Recurso|metadados do modo de procura|Os procedimentos armazenados nativamente compilados não oferecem suporte aos metadados do modo de procura. Verifique se a opção de sessão `NO_BROWSETABLE` está definida como OFF.|  
|Recurso|DELETE com a cláusula FROM|A cláusula `FROM` não tem suporte para as instruções `DELETE` com uma fonte de tabela em procedimentos armazenados compilados de modo nativo.<br /><br /> `DELETE` com a cláusula `FROM` tem suporte quando ela é usada para indicar a tabela de onde haverá exclusão.|  
|Recurso|UPDATE com a cláusula FROM|A cláusula `FROM` não tem suporte para as instruções `UPDATE` em procedimentos armazenados nativamente compilados.|  
|Recurso|procedimentos temporários|Os procedimentos armazenados temporários não podem ser compilados nativamente. Crie um procedimento armazenado nativamente compilado permanente ou um procedimento armazenado do [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado temporário.|  
|Nível de isolamento|READ UNCOMMITTED|O nível de isolamento READ UNCOMMITTED não tem suporte para procedimentos armazenados nativamente compilados. Use um nível de isolamento com suporte, como SNAPSHOT.|  
|Nível de isolamento|READ COMMITTED|O nível de isolamento READ UNCOMMITTED não tem suporte para procedimentos armazenados nativamente compilados. Use um nível de isolamento com suporte, como SNAPSHOT.|  
|Recurso|tabelas temporárias|As tabelas em tempdb não podem ser usadas em procedimentos armazenados nativamente compilados. Em vez disso, use uma variável de tabela ou uma tabela com otimização de memória com DURABILITY=SCHEMA_ONLY.|  
|Recurso|MARS|O MARS (Vários Conjuntos de Resultados Ativos) não tem suporte com procedimentos armazenados nativamente compilados. Esse erro também pode indicar uso de servidor vinculado. O servidor vinculado pode usar MARS. Servidores vinculados não têm suporte com procedimentos armazenados nativamente compilados. Conecte-se diretamente ao servidor e ao banco de dados que hospeda os procedimentos armazenados nativamente compilados.|  
|Recurso|DTC|As tabelas com otimização de memória e os procedimentos armazenados nativamente compilados não podem ser acessados de transações distribuídas. Em vez disso, use transações SQL.|  
|Recurso|ordenação non-bin2|As operações de comparação, classificação, entre outras, em cadeias de caracteres em procedimentos armazenados nativamente compilados exigem o uso de uma ordenação BIN2. Use a cláusula COLLATE ou colunas e variáveis com uma ordenação adequada. Para obter mais informações, consulte [Páginas de código de ordenações](../../database-engine/collations-and-code-pages.md).|  
|Recurso|Truncamento de cadeias de caracteres com uma ordenação SC.|As cadeias de caracteres com uma ordenação `_SC` usam a codificação UTF-16. A conversão de um valor n(var)char em um valor n(var)char com um comprimento curto envolve truncamento. Isso não tem suporte para valores UTF-16 em procedimentos armazenados nativamente compilados. Evite o truncamento de cadeias de caracteres UTF-16.|  
|Recurso|EXECUTE WITH RECOMPILE|A opção `WITH RECOMPILE` não tem suporte para procedimentos armazenados nativamente compilados.|  
|Recurso|LEN e SUBSTRING com um argumento em uma ordenação SC|As cadeias de caracteres com uma ordenação _SC usam a codificação UTF-16. As funções internas LEN e SUBSTRING, quando usadas nos procedimentos armazenados compilados de modo nativo, não oferecem suporte à codificação UTF-16. Use uma ordenação diferente ou evite usar essas funções.|  
|Recurso|Execução da conexão de administrador dedicada.|Os procedimentos armazenados nativamente compilados não podem ser executados da DAC (conexão do administrador dedicado). Use uma conexão normal.|  
|Operação|ALTER PROCEDURE|Os procedimentos armazenados nativamente compilados não podem ser alterados. Para alterar a definição do procedimento, descarte e recrie o procedimento armazenado.|  
|Operação|ponto de salvamento|Os procedimentos armazenados nativamente compilados não podem ser invocados de transações que tenham um ponto de salvamento ativo. Remova o ponto de salvamento da transação.|  
|Operação|ALTER AUTHORIZATION|Não há suporte para alteração do proprietário de uma tabela com otimização de memória ou procedimentos armazenados nativamente compilados existentes. Descarte e recrie a tabela ou o procedimento para alterar a propriedade.|  
|Operador|OPENROWSET|Não há suporte para esse operador. Remova `OPENROWSET` do procedimento armazenado nativamente compilado.|  
|Operador|OPENQUERY|Não há suporte para esse operador. Remova `OPENQUERY` do procedimento armazenado nativamente compilado.|  
|Operador|OPENDATASOURCE|Não há suporte para esse operador. Remova `OPENDATASOURCE` do procedimento armazenado nativamente compilado.|  
|Operador|OPENXML|Não há suporte para esse operador. Remova `OPENXML` do procedimento armazenado nativamente compilado.|  
|Operador|CONTAINSTABLE|Não há suporte para esse operador. Remova `CONTAINSTABLE` do procedimento armazenado nativamente compilado.|  
|Operador|FREETEXTTABLE|Não há suporte para esse operador. Remova `FREETEXTTABLE` do procedimento armazenado nativamente compilado.|  
|Recurso|funções com valor de tabela|As funções com valor de tabela não podem ser referenciadas de procedimentos armazenados nativamente compilados. Uma solução possível para essa restrição é adicionar a lógica das funções com valor de tabela ao corpo do procedimento.|  
|Operador|CHANGETABLE|Não há suporte para esse operador. Remova `CHANGETABLE` do procedimento armazenado nativamente compilado.|  
|Operador|GOTO|Não há suporte para esse operador. Use outras construções de procedimento, como WHILE.|  
|Operador|EXECUTE, INSERT EXEC|Não há suporte para o aninhamento de procedimentos armazenados nativamente compilados. As operações necessárias podem ser especificadas em linha, como parte da definição do procedimento armazenado.|  
|Operador|OFFSET|Não há suporte para esse operador. Remova `OFFSET` do procedimento armazenado nativamente compilado.|  
|Operador|UNION|Não há suporte para esse operador. Remova `UNION` do procedimento armazenado nativamente compilado. A combinação de vários conjuntos de resultados em um único conjunto de resultados pode ser feita usando uma variável de tabela.|  
|Operador|INTERSECT|Não há suporte para esse operador. Remova `INTERSECT` do procedimento armazenado nativamente compilado. Em alguns casos, um INNER JOIN pode ser usado para obter o mesmo resultado.|  
|Operador|EXCEPT|Não há suporte para esse operador. Remova `EXCEPT` do procedimento armazenado nativamente compilado.|  
|Operador|OUTER JOIN|Não há suporte para esse operador. Remova `OUTER JOIN` do procedimento armazenado nativamente compilado. Para obter mais informações, consulte [implementando uma junção externa](implementing-an-outer-join.md).|  
|Operador|APPLY|Não há suporte para esse operador. Remova `APPLY` do procedimento armazenado nativamente compilado.|  
|Operador|PIVOT|Não há suporte para esse operador. Remova `PIVOT` do procedimento armazenado nativamente compilado.|  
|Operador|UNPIVOT|Não há suporte para esse operador. Remova `UNPIVOT` do procedimento armazenado nativamente compilado.|  
|Operador|OR, IN|A disjunção (OR, IN) não tem suporte na cláusula WHERE das consultas em procedimentos armazenados compilados de modo nativo. Crie consultas para cada um dos casos.|  
|Operador|CONTAINS|Não há suporte para esse operador. Remova `CONTAINS` do procedimento armazenado nativamente compilado.|  
|Operador|FREETEXT|Não há suporte para esse operador. Remova `FREETEXT` do procedimento armazenado nativamente compilado.|  
|Operador|NOT|Não há suporte para esse operador. Remova `NOT` do procedimento armazenado nativamente compilado. Em alguns casos, `NOT` pode ser substituído por desigualdade. Por exemplo, `NOT a=b` pode ser substituído por `a!=b`.|  
|Operador|TSEQUAL|Não há suporte para esse operador. Remova `TSEQUAL` do procedimento armazenado nativamente compilado.|  
|Operador|LIKE|Não há suporte para esse operador. Remova `LIKE` do procedimento armazenado nativamente compilado.|  
|Operador|NEXT VALUE FOR|As sequências não podem referenciadas dentro de procedimentos armazenados nativamente compilados. Obtenha o valor usando [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado e transmita-o ao procedimento armazenado nativamente compilado. Para obter mais informações, veja [Implementando IDENTITY em uma tabela com otimização de memória](implementing-identity-in-a-memory-optimized-table.md).|  
|Opção Set|*opção*|As opções SET não podem ser alteradas dentro de procedimentos armazenados nativamente compilados. Algumas opções podem ser definidas com a instrução BEGIN ATOMIC. Para obter mais informações, confira a seção sobre blocos atômicos em [Procedimentos armazenados compilados de modo nativo](../in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Operando|TABLESAMPLE|Não há suporte para esse operador. Remova `TABLESAMPLE` do procedimento armazenado nativamente compilado.|  
|Opção|RECOMPILE|Os procedimentos armazenados nativamente compilados são compilados no tempo de criação. Para recompilar um procedimento armazenado nativamente compilado, descarte-o e recrie-o. Remova `RECOMPILE` da definição do procedimento.|  
|Opção|ENCRYPTION|Não há suporte para essa opção. Remova `ENCRYPTION` da definição do procedimento.|  
|Opção|FOR REPLICATION|Os procedimentos armazenados nativamente compilados não podem ser criados para replicação. Remova `FOR REPLICATION` da definição de procedimento.|  
|Opção|FOR XML|Não há suporte para essa opção. Remova `FOR XML` do procedimento armazenado nativamente compilado.|  
|Opção|FOR BROWSE|Não há suporte para essa opção. Remova `FOR BROWSE` do procedimento armazenado nativamente compilado.|  
|Dica de junção|HASH, MERGE|Os procedimentos armazenados nativamente compilados oferecem suporte somente a junções de loops aninhados. Não há suporte para junções de hash e mesclagem. Remova a dica de junção.|  
|Dica de consulta|*Dica de consulta*|Essa dica de consulta não está dentro de procedimentos armazenados nativamente compilados. Para obter dicas de consulta com suporte, veja [Dicas de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query).|  
|Opção|DISTINCT|Não há suporte para essa opção. Remova `DISTINCT` da consulta no procedimento armazenado nativamente compilado.|  
|Opção|PERCENT|Essa opção não tem suporte com cláusulas `TOP`. Remova `PERCENT` da consulta no procedimento armazenado nativamente compilado.|  
|Opção|WITH TIES|Essa opção não tem suporte com cláusulas `TOP`. Remova `WITH TIES` da consulta no procedimento armazenado nativamente compilado.|  
|Função de agregação|*Função de agregação*|Não há suporte para essa cláusula. Para obter mais informações sobre procedimentos armazenados compilados de modo nativo, veja [Procedimentos armazenados compilados de modo nativo](../in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Função de classificação|*Função de classificação*|As funções de classificação não têm suporte em procedimentos armazenados nativamente compilados. Remova-as da definição de procedimento.|  
|Função|*Função*|Não há suporte para essa função. Remova-a do procedimento armazenado nativamente compilado.|  
|de|*Privacidade*|Não há suporte para essa instrução. Remova-a do procedimento armazenado nativamente compilado.|  
|Recurso|MIN e MAX usados com cadeias de caracteres e binários|As funções de agregação `MIN` e `MAX` não podem ser usadas para valores de cadeias de caracteres binários e caracteres dentro de procedimentos armazenados nativamente compilados.|  
|Recurso|GROUP BY sem função de agregação|Em procedimentos armazenados compilados de modo nativo, quando uma consulta tem uma cláusula `GROUP BY`, a consulta também deve usar uma função de agregação na cláusula SELECT ou HAVING. Adicione uma função de agregação à consulta.|  
|Recurso|GROUP BY ALL|ALL não pode ser usado com cláusulas GROUP BY em procedimentos armazenados compilados de modo nativo. Remova ALL da cláusula GROUP BY.|  
|Recurso|GROUP BY ()|Não suporte para o agrupamento por uma lista vazia. Remova a cláusula GROUP BY ou inclua colunas na lista de agrupamentos.|  
|Recurso|ROLLUP|`ROLLUP` não pode ser usado com cláusulas `GROUP BY` em procedimentos armazenados nativamente compilados. Remova `ROLLUP` da definição do procedimento.|  
|Recurso|CUBE|`CUBE` não pode ser usado com cláusulas `GROUP BY` em procedimentos armazenados nativamente compilados. Remova `CUBE` da definição do procedimento.|  
|Recurso|GROUPING SETS|`GROUPING SETS` não pode ser usado com cláusulas `GROUP BY` em procedimentos armazenados nativamente compilados. Remova `GROUPING SETS` da definição do procedimento.|  
|Recurso|BEGIN TRANSACTION, COMMIT TRANSACTION e ROLLBACK TRANSACTION|Use blocos ATOMIC para controlar transações e tratamento de erros. Para obter mais informações, veja [Blocos atômicos](atomic-blocks-in-native-procedures.md).|  
|Recurso|Declarações de variável de tabela embutidas.|As variáveis de tabela devem referenciar explicitamente os tipos de tabela com otimização de memória definidos. Você deve criar um tipo de tabela com otimização de memória e usar esse tipo para a declaração variável, em vez de especificar o tipo embutido.|  
|Recurso|sp_recompile|Não há suporte para a recompilação de procedimentos armazenados compilados de modo nativo. Remova e recrie o procedimento.|  
|Recurso|EXECUTE AS CALLER|A cláusula `EXECUTE AS` é necessária. Mas, não há suporte para `EXECUTE AS CALLER`. Use `EXECUTE AS OWNER` , `EXECUTE AS` *User*ou `EXECUTE AS SELF` .|  
|Recurso|Tabelas baseadas em disco|As tabelas baseadas em disco não podem ser acessadas nos procedimentos armazenados compilados de modo nativo. Remova as referências a tabelas baseadas em disco dos procedimentos armazenados compilados de modo nativo. Ou migre as tabelas baseadas em disco para tabelas com otimização de memória.|  
|Recurso|Exibições|As exibições não podem ser acessadas nos procedimentos armazenados compilados de modo nativo. Em vez das exibições, referencie as tabelas base subjacentes.|  
|Recurso|Funções com valor de tabela|As funções com valor de tabela não podem ser acessadas nos procedimentos armazenados compilados de modo nativo. Remova as referências a funções com valor de tabela do procedimento armazenado compilado de modo nativo.|  
  
## <a name="transactions-that-access-memory-optimized-tables"></a>Transações que acessam tabelas com otimização de memória  
 A tabela a seguir lista os recursos e as palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem aparecer no texto da mensagem de um erro que envolve transações que acessam tabelas com otimização de memória, bem como a ação corretiva para resolver o erro.  
  
|Type|Nome|Resolução|  
|----------|----------|----------------|  
|Recurso|ponto de salvamento|Não há suporte para a criação de pontos de salvamento explícitos em transações que acessam tabelas com otimização de memória.|  
|Recurso|transação associada|As sessões associadas não podem participar de transações que acessam tabelas com otimização de memória. Não associe a sessão antes de executar o procedimento.|  
|Recurso|DTC|As transações que acessam tabelas com otimização de memória não podem ser transações distribuídas.|  
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)  
  
  
