---
title: Gerenciar FileTables | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], security
- FileTables [SQL Server], managing access
ms.assetid: 93af982c-b4fe-4be0-8268-11f86dae27e1
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 22af72edfc8fb5e3f17544de3f30d1b1e3aa09c7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="manage-filetables"></a>Gerenciar FileTables
  Descreve tarefas administrativas comuns para gerenciar FileTables.  
  
##  <a name="HowToEnumerate"></a> Como obter uma lista de FileTables e objetos relacionados  
 Para obter uma lista de FileTables, consulte um das exibições do catálogo a seguir:  
  
-   [sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
  
-   [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) (Verifique o valor da coluna **is_filetable**.)  
  
```sql  
SELECT * FROM sys.filetables;  
GO  
  
SELECT * FROM sys.tables WHERE is_filetable = 1;  
GO  
```  
  
 Para obter uma lista dos objetos definidos pelo sistema que foram criados quando as FileTables associadas foram criadas, consulte a exibição de catálogo [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md).  
  
```sql  
SELECT object_id, OBJECT_NAME(object_id) AS 'Object Name'  
FROM sys.filetable_system_defined_objects;  
GO  
```  
  
##  <a name="BasicsDisabling"></a> Desabilitando e reabilitando o acesso não transacional no nível de banco de dados  
 Para adquirir o acesso exclusivo que é necessário para determinadas tarefas administrativas, talvez seja necessário desabilitar temporariamente o acesso não transacional.  
  
 **Comportamento da instrução ALTER DATABASE ao alterar o nível de acesso não transacional**  
  
-   Quando você definir o acesso não transacional como READ_ONLY ou OFF, o comando ALTER DATABASE não retornará o controle ao usuário enquanto houver identificadores de arquivos abertos em conflito com a operação solicitada. Os identificadores de arquivos que estão em conflito com esta operação incluem o seguinte:  
  
    -   Quando você está definindo o acesso como **NONE**, todos os identificadores de arquivos abertos.  
  
    -   Quando você define o acesso como **READ_ONLY**, todos os identificadores de arquivos são abertos para o acesso de gravação.  
  
     Para obter informações sobre como eliminar identificadores de arquivos abertos, consulte [Eliminando identificadores de arquivos abertos associados a um FileTable](#BasicsKilling) neste tópico.  
  
     Se o comando ALTER DATABASE for cancelado ou terminar com um tempo limite, o nível de acesso transacional não será alterado.  
  
-   Se você chamar a instrução ALTER DATABASE com uma cláusula WITH \<termination> (ROLLBACK AFTER integer [ SECONDS ] | ROLLBACK IMMEDIATE | NO_WAIT), todos os identificadores de arquivos não transacionais abertos serão eliminados.  
  
> [!WARNING]  
>  A eliminação de identificadores de arquivos abertos pode levar os usuários a perderem dados não salvos. Esse comportamento é consistente com o comportamento do próprio sistema de arquivos.  
  
 **Efeitos de desabilitar o acesso não transacional**  
  
 A alteração do nível de acesso não transacional no nível de banco de dados tem os seguintes efeitos nos diretórios de FileTable sob o diretório em nível de banco de dados:  
  
-   Quando você definir o acesso como **NONE**, todos os diretórios FileTable e seu conteúdo não ficará mais acessível nem visível.  
  
-   Quando você define o acesso como **READ_ONLY**, todos os diretórios de FileTable e seu conteúdo também são somente leitura.  
  
 A desabilitação de FILESTREAM no nível de instância tem os seguintes efeitos nos diretórios em nível de banco de dados nessa instância e nos diretórios de FileTable sob eles:  
  
-   Nenhum dos diretórios em nível de banco de dados na instância estará visível se FILESTREAM for desabilitado no nível de instância.  
  
###  <a name="HowToDisable"></a> Como desabilitar e reabilitar o acesso não transacional no nível de banco de dados  
 Para obter mais informações, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 **Para desabilitar o acesso não transacional**  
 Chame a instrução **ALTER DATABASE** e defina o valor de **NON_TRANSACTED_ACCESS** como **READ_ONLY** ou **OFF**.  
  
```sql  
-- Disable write access.  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = READ_ONLY );  
GO  
  
-- Disable non-transactional access.  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = OFF );  
GO  
```  
  
 **Para reabilitar o acesso não transacional**  
 Chame a instrução **ALTER DATABASE** e defina o valor de **NON_TRANSACTED_ACCESS** como **FULL**.  
  
```sql  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL );  
GO  
```  
  
###  <a name="visible"></a> Como garantir a visibilidade do FileTables em um banco de dados  
 Um diretório em nível de banco de dados e os diretórios FileTable sob ele estarão visíveis quando todas essa condições forem atendidas  
  
1.  O FILESTREAM está habilitado no nível de instância.  
  
2.  O acesso não transacional está habilitado no nível de banco de dados.  
  
3.  Um diretório válido foi especificado ao nível de banco de dados.  
  
##  <a name="BasicsEnabling"></a> Desabilitando e reabilitando o namespace FileTable no nível de tabela  
 Desabilitar o namespace FileTable desabilita todos os gatilhos e restrições definidos pelo sistema que foram criados com o FileTable. Isso é útil em casos em que um FileTable precisa ser reorganizado em grande escala usando operações [!INCLUDE[tsql](../../includes/tsql-md.md)] sem recorrer à imposição de semântica de FileTable. Entretanto, essas operações podem deixar FileTable em um estado inconsistente e podem impedir a reabilitação do namespace FileTable.  
  
 A desabilitação de um namespace FileTable tem os resultados seguintes:  
  
-   As colunas e dados de FileTable não são fisicamente removidos da tabela.  
  
-   O diretório de FileTable, e seus arquivos e diretórios, desaparecem do sistema de arquivo e não estão disponíveis para o acesso de E/S de arquivo.  
  
-   As colunas de FileTable definidas pelo sistema não podem ser removidas e recriadas; caso contrário, contudo elas se comportam como qualquer outra coluna em operações DML.  
  
-   Identificadores de arquivos abertos impedem que as restrições de FileTable sejam desabilitadas, pois essa operação requer um bloqueio de esquema na tabela.  
  
-   A execução de toda a semântica de FileTable, inclusive restrições definidas por sistema e gatilhos, é interrompida depois que o namespace FileTable é desabilitado.  
  
 A reabilitação de um namespace FileTable tem os seguintes resultados:  
  
-   É verificada a consistência de FileTable. Se forem encontradas inconsistências, um erro ocorrerá e o FileTable permanecerá desabilitado; caso contrário, o FileTable será reabilitado.  
  
-   A imposição da semântica de FileTable, inclusive restrições definidas pelo sistema e gatilhos, é restaurada.  
  
-   O diretório de FileTable, e seus arquivos e diretórios, ficam visíveis no sistema de arquivo e ficam disponíveis para o acesso de E/S de arquivo.  
  
###  <a name="HowToEnableNS"></a> Como desabilitar e reabilitar o namespace FileTable no nível de tabela  
 Chame a instrução ALTER TABLE com a opção **{ ENABLE | DISABLE } FILETABLE_NAMESPACE** .  
  
 **Para desabilitar o namespace da FileTable**  
 ```sql  
ALTER TABLE filetable_name  
DISABLE FILETABLE_NAMESPACE;  
GO  
```  
  
 **Para reabilitar o namespace da FileTable**  
 ```sql  
ALTER TABLE filetable_name  
ENABLE FILETABLE_NAMESPACE;  
GO  
```  
  
##  <a name="BasicsKilling"></a> Eliminando identificadores de arquivos abertos associados a um FileTable  
 Os identificadores abertos para os arquivos armazenados em uma FileTable podem impedir o acesso exclusivo que é necessário para determinadas tarefas administrativas. Para habilitar tarefas urgentes, você poderá precisar eliminar identificadores de arquivos abertos associados a uma ou mais FileTables.  
  
> [!WARNING]  
>  A eliminação de identificadores de arquivos abertos pode levar os usuários a perderem dados não salvos. Esse comportamento é consistente com o comportamento do próprio sistema de arquivos.  
  
###  <a name="HowToListOpen"></a> Como obter uma lista de identificadores de arquivos abertos associados a um FileTable  
 Consulte a exibição de catálogo [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).  
  
```sql  
SELECT * FROM sys.dm_filestream_non_transacted_handles;  
GO  
```  
  
###  <a name="HowToKill"></a> Como eliminar identificadores de arquivos abertos associados a um FileTable  
 Chame o procedimento armazenado [sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md) com os argumentos apropriados para eliminar todos os identificadores de arquivos abertos no banco de dados ou na FileTable, ou para eliminar um identificador específico.  
  
```sql  
USE database_name;  
  
-- Kill all open handles in all the filetables in the database.  
EXEC sp_kill_filestream_non_transacted_handles;  
GO  
  
-- Kill all open handles in a single filetable.  
EXEC sp_kill_filestream_non_transacted_handles @table_name = 'filetable_name';  
GO  
  
-- Kill a single handle.  
EXEC sp_kill_filestream_non_transacted_handles @handle_id = integer_handle_id;  
GO  
```  
  
###  <a name="HowToIdentifyLocks"></a> Como identificar os bloqueios mantidos por FileTables  
 A maioria dos bloqueios feitos por FileTables correspondem a arquivos abertos por aplicativos.  
  
 **Para identificar arquivos abertos e os bloqueios associados**  
 Una o campo **request_owner_id** à exibição de gerenciamento dinâmico [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md) com o campo **fcb_id** em [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md). Em alguns casos, o bloqueio não corresponde a um único identificador de arquivo aberto.  
  
```sql  
SELECT opened_file_name  
FROM sys.dm_filestream_non_transacted_handles  
WHERE fcb_id IN  
    ( SELECT request_owner_id FROM sys.dm_tran_locks );  
GO  
```  
  
##  <a name="BasicsSecurity"></a> Segurança de FileTable  
 Os arquivos e diretórios armazenados em FileTables só ficam protegidos pela segurança do SQL Server. A segurança com base em tabela e coluna é imposta para acesso de sistema de arquivos, assim como o acesso [!INCLUDE[tsql](../../includes/tsql-md.md)] . Não há suporte para configurações de ACL e APIs de segurança do sistema de arquivos Windows.  
  
 As permissões de segurança e acesso aplicáveis a grupos de arquivos e contêineres FILESTREAM também se aplicam a FileTables, desde que os dados de arquivos estejam armazenados como uma coluna FILESTREAM no FileTable.  
  
 **Segurança de FileTable e acesso Transact-SQL**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] acesso aos dados em FileTables é protegido da mesma maneira como em qualquer outra tabela. São feitas verificações de segurança apropriadas em nível de tabela e de coluna para cada operação que acessa ou altera os dados.  
  
 **Segurança de FileTable e acesso ao sistema de arquivos**  
 APIs do sistema de arquivos exigem permissões apropriadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na linha inteira no FileTable (ou seja, permissão em nível de tabela) para abrir um identificador em um arquivo ou diretório armazenado no FileTable. Se o usuário não tiver a permissão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apropriada em qualquer coluna do FileTable, o acesso ao sistema de arquivos será negado.  
  
##  <a name="OtherBackup"></a> Backup e FileTables  
 Quando você usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer backup de um FileTable, o backup dos dados FILESTREAM é feito com os dados estruturados no banco de dados. Se você não desejar fazer backup de dados FILESTREAM com dados relacionais, poderá usar um backup parcial para excluir grupos de arquivos FILESTREAM.  
  
 **Consistência transacional de backups de FileTable**  
  
 Muitas ferramentas e operações administrativas, (inclusive backup, backup de log e replicação transacional) leem dados transacionalmente consistentes lendo os logs de transações. Neste momento, eles leem quaisquer dados FILESTREAM atualizados como parte de uma transação. Quando o acesso não transacional não está habilitado no nível de banco de dados, essas ferramentas e operações funcionam com total consistência transacional.  
  
 Entretanto, quando o acesso completo não transacional estiver habilitado, uma FileTable poderá conter dados que foram atualizados mais recentemente (por meio de uma atualização não transacional) do que a transação que a ferramenta ou o processo está lendo no log de transação. Isso significa que uma operação de restauração pontual em uma transação específica pode conter dados FILESTREAM mais recentes do que aquela transação. Esse é o comportamento esperado quando são permitidas atualizações não transacionais em FileTables.  
  
##  <a name="Monitor"></a> Recursos do SQL Server Profiler e FileTables  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler pode capturar as operações Abrir Arquivo e Fechar Arquivo do Windows no rastreamento gerado para arquivos que são armazenados em um FileTable.  
  
##  <a name="OtherAuditing"></a> Auditoria e FileTables  
 A FileTable pode ser auditada como qualquer outra tabela. Entretanto, os padrões de acesso do Win32 não são operações baseadas em conjunto. Uma única ação no sistema de arquivos é traduzida em várias operações DML Transact-SQL. Por exemplo, a abertura de um arquivo no Microsoft Word se traduz em várias operações de abertura/fechamento/criação/renomeação/exclusão e em atividades DML Transact-SQL correspondentes. Isso resulta em registros de auditoria detalhados, onde é difícil correlacionar registros entre ações do sistema de arquivos e registros de auditoria DML Transact-SQL correspondentes.  
  
##  <a name="OtherDBCC"></a> DBCC e FileTables  
 Você pode usar DBCC CHECKCONSTRAINTS para validar as restrições em uma FileTable, inclusive restrições definidas pelo sistema.  
  
## <a name="see-also"></a>Consulte também  
 [Compatibilidade do FileTable com outros recursos do SQL Server](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)   
 [DDL, funções, procedimentos armazenados e exibições de FileTable](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
