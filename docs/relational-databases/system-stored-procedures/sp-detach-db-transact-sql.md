---
title: sp_detach_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_db
- sp_detach_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_db
- detaching databases [SQL Server]
ms.assetid: abcb1407-ff78-4c76-b02e-509c86574462
author: stevestein
ms.author: sstein
ms.openlocfilehash: ec7758ad2f9443ad29f0da799e3f286612f95cab
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278185"
---
# <a name="sp_detach_db-transact-sql"></a>sp_detach_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desanexa um banco de dados que não está em uso atualmente em uma instância de servidor e, opcionalmente, executa UPDATE STATISTICS em todas as tabelas antes de desanexar.  
  
> [!IMPORTANT]  
>  Para que um banco de dados replicado seja desanexado, é preciso que ele seja não publicado. Para obter mais informações, consulte "Comentários", posteriormente neste tópico.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_detach_db [ @dbname= ] 'database_name'   
    [ , [ @skipchecks= ] 'skipchecks' ]   
    [ , [ @keepfulltextindexfile = ] 'KeepFulltextIndexFile' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'database_name'` é o nome do banco de dados a ser desanexado. *database_name* é um valor **sysname** , com um valor padrão de NULL.  
  
`[ @skipchecks = ] 'skipchecks'` especifica se a estatística de atualização deve ser ignorada ou executada. *skipchecks* é um valor **nvarchar (10)** , com um valor padrão de NULL. Para ignorar as estatísticas de atualização, especifique **true**. Para executar explicitamente UPDATE STATISTICs, especifique **false**.  
  
 Por padrão, UPDATE STATISTICS é executado para atualizar as informações sobre os dados nas tabelas e os índices. A execução de UPDATE STATISTICS é útil para bancos de dados que serão movidos para mídias somente leitura.  
  
`[ @keepfulltextindexfile = ] 'KeepFulltextIndexFile'` especifica que o arquivo de índice de texto completo associado ao banco de dados que está sendo desanexado não será removido durante a operação de desanexação do banco de dados. *Keepfulltextindexfile* é um valor **nvarchar (10)** com um padrão de **true**. Se *keepfulltextindexfile* for **false**, todos os arquivos de índice de texto completo associados ao banco de dados e os metadados do índice de texto completo serão descartados, a menos que o banco de dados seja somente leitura. Se for NULL ou **true**, os metadados relacionados a texto completo serão mantidos.  
  
> [!IMPORTANT]
>  O parâmetro **\@keepfulltextindexfile** será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não use esse parâmetro em desenvolvimentos novos e modifique, assim que possível, os aplicativos que atualmente o usam.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Quando um banco de dados é desanexado, todos os metadados são descartados. Se o banco de dados for o banco de dados padrão de qualquer conta de logon, o **mestre** se tornará seu banco de dados padrão.  
  
> [!NOTE]  
>  Para obter informações sobre como exibir o banco de dados padrão de todas as contas de logon, consulte [Transact-SQL &#40;&#41;sp_helplogins](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md). Se você tiver as permissões necessárias, poderá usar [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) para atribuir um novo banco de dados padrão a um logon.  
  
## <a name="restrictions"></a>Restrições  
 Um banco de dados não pode ser desanexado se algum dos seguintes fatores for verdadeiro:  
  
-   O banco de dados está atualmente em uso. Para obter mais informações, consulte "Obtendo acesso exclusivo”, posteriormente neste tópico.  
  
-   Se duplicado, o banco de dados será publicado.  
  
     Antes de poder desanexar o banco de dados, você deve desabilitar a publicação executando [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
  
    > [!NOTE]  
    >  Se não for possível usar **sp_replicationdboption**, você poderá remover a replicação executando [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
-   Há um instantâneo do banco de dados no banco de dados.  
  
     Antes de poder desanexar o banco de dados, você deve descartar todos os seus instantâneos. Para obter mais informações, veja [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
    > [!NOTE]  
    >  Um instantâneo do banco de dados não pode ser desanexado ou anexado.  
  
-   O banco de dados está sendo espelhado.  
  
     O banco de dados não pode ser desanexado até que a sessão de espelhamento de banco de dados seja encerrada. Para obter mais informações, veja [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
-   O banco de dados é suspeito.  
  
     É preciso colocar um banco de dados suspeito em modo de emergência antes de poder desanexá-lo. Para obter mais informações sobre como colocar um banco de dados em modo de emergência, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   O banco de dados é um banco de dados de sistema.  
  
## <a name="obtaining-exclusive-access"></a>Obtendo acesso exclusivo  
 A desanexação de um banco de dados exige acesso exclusivo ao banco de dados. Se o banco de dados a ser dexanexado estiver em uso, antes que ele possa ser desanexado, defina o banco de dados como modo SINGLE_USER para obter acesso exclusivo.

 Antes de definir o banco de dados como SINGLE_USER, verifique se a opção AUTO_UPDATE_STATISTICS_ASYNC está definida como OFF. Quando esta opção está definida como ON, o thread em segundo plano usado para a atualização de estatísticas estabelece uma conexão com o banco de dados e não será possível acessar o banco de dados em modo de usuário único. Para obter mais informações, consulte [definir um banco de dados para o modo de usuário único](../databases/set-a-database-to-single-user-mode.md).

 Por exemplo, a instrução `ALTER DATABASE` a seguir obtém acesso exclusivo ao banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] depois que todos os usuários atuais se desconectam do banco de dados.  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  Para forçar os usuários atuais do banco de dados imediatamente ou dentro de um determinado número de segundos, use também a opção de reversão: ALTER DATABASE *database_name* SET SINGLE_USER WITH ROLLBACK *rollback_option*. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="reattaching-a-database"></a>Reanexando um banco de dados  
 Os arquivos desanexados permanecem e podem ser anexados novamente com o uso de CREATE DATABASE (com a opção FOR ATTACH ou FOR ATTACH_REBUILD_LOG). Os arquivos podem ser movidos para outro servidor, onde podem ser anexados.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **sysadmin** ou à associação na função **db_owner** do banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir desanexa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] com *skipchecks* definido como true.  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
 O exemplo a seguir desanexa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] e mantém os arquivos de índice de texto completo e os metadados de índice de texto completo. Esse comando executa UPDATE STATISTICS, que é o comportamento padrão.  
  
```  
exec sp_detach_db @dbname='AdventureWorks2012'  
    , @keepfulltextindexfile='true';  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Desanexar um banco de dados](../../relational-databases/databases/detach-a-database.md)  
  
  
