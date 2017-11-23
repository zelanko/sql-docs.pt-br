---
title: DROP DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE
- DROP_DATABASE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], deleting
- removing databases
- database snapshots [SQL Server], removing
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- DROP DATABASE statement
- database removal [SQL Server], DROP DATABASE statement
ms.assetid: 477396a9-92dc-43c9-9b97-42c8728ede8e
caps.latest.revision: "83"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 6e963031c1d9f27293a2f0786e7f0ce19183f038
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-database-transact-sql"></a>DROP DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Remove um ou mais bancos de dados de usuário ou instantâneos do banco de dados de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- SQL Server Syntax  
DROP DATABASE [ IF EXISTS ] { database_name | database_snapshot_name } [ ,...n ] [;]  
```  
  
```  
-- Azure SQL Database, Azure SQL Data Warehouse and Parallel Data Warehouse Syntax   
DROP DATABASE database_name [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Condicionalmente descarta o banco de dados somente se ele já existe.  
  
 *database_name*  
 Especifica o nome do banco de dados a ser removido. Para exibir uma lista de bancos de dados, use o [sys. Databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) exibição do catálogo.  
  
 *database_snapshot_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o nome de um instantâneo do banco de dados a ser removido.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Um banco de dados pode ser removido independentemente de seu estado: offline, somente leitura, suspeito e assim por diante. Para exibir o estado atual de um banco de dados, use o **sys. Databases** exibição do catálogo.  
  
 Um banco de dados cancelado poderá ser recriado somente por meio da restauração de um backup. Não é possível efetuar backup de instantâneos do banco de dados, portanto, eles não podem ser restaurados.  
  
 Quando um banco de dados é descartado, o [banco de dados mestre](../../relational-databases/databases/master-database.md) deve ser feito backup.  
  
 O descarte de um banco de dados exclui o banco de dados de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exclui os arquivos de disco físicos usados pelo banco de dados. Se o banco de dados ou qualquer um de seus arquivos estiverem offline quando forem cancelados, os arquivos em disco não serão excluídos. Esses arquivos podem ser excluídos manualmente usando o Windows Explorer. Para remover um banco de dados do servidor atual sem excluir os arquivos do sistema de arquivos, use [sp_detach_db](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md).  
  
> [!WARNING]  
>  Descartar um banco de dados com FILE_SNAPSHOT backups associados a ele terá êxito, mas os arquivos de banco de dados que tenham instantâneos associados não serão excluídos para evitar a anulação os backups que faz referência a esses arquivos de banco de dados. O arquivo será truncado, mas não serão fisicamente excluído para manter os backups FILE_SNAPSHOT intactos. Para obter mais informações, veja [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O descarte de um instantâneo de banco de dados o exclui de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exclui os arquivos físicos esparsos do Sistema de Arquivos NTFS utilizados pelo instantâneo. Para obter informações sobre como usar arquivos esparsos por instantâneos do banco de dados, consulte [instantâneos de banco de dados &#40; SQL Server &#41; ](../../relational-databases/databases/database-snapshots-sql-server.md). O cancelamento de um instantâneo do banco de dados limpa o cache de plano para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrência(s) de liberação de armazenamento em cache '% s' (parte do cache de planos) devido à manutenção do banco de dados ou operações de reconfiguração". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.  
  
## <a name="interoperability"></a>Interoperabilidade  
  
### <a name="sql-server"></a>SQL Server  
 Para cancelar um banco de dados publicado para replicação transacional ou publicado ou inscrito para replicação de mesclagem, você deve primeiro remover a replicação do banco de dados. Se um banco de dados estiver danificado ou não for possível remover a replicação primeiro ou ambos, na maioria dos casos você ainda pode cancelar o banco de dados usando ALTER DATABASE para definir o banco de dados offline e depois cancelá-lo.  
  
 Se o banco de dados estiver envolvido em envio de logs, remova o envio do log antes de cancelá-lo. Para obter mais informações, consulte [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 [Bancos de dados de sistema](../../relational-databases/databases/system-databases.md) não pode ser descartado.  
  
 Uma instrução DROP DATABASE deve ser executada no modo de confirmação automática e não é permitida uma transação explícita ou implícita. O modo de confirmação automática é o modo padrão de gerenciamento de transações.  
  
 Você não pode cancelar um banco de dados que estiver sendo utilizado. Isso significa abrir para leitura ou gravação por qualquer usuário. Para remover usuários do banco de dados, use ALTER DATABASE para definir o banco de dados como SINGLE_USER.  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Qualquer instantâneo de banco de dados em um banco de dados deve ser cancelado antes que o banco de dados seja cancelado.  
  
 Descartar um banco de dados permite para o Stretch Database não remove os dados remotos. Se você deseja excluir os dados remotos, você precisa removê-lo manualmente.  
  
### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 Você deve estar conectado ao banco de dados mestre para descartar um banco de dados.
  
 A instrução DROP DATABASE deve ser a única instrução em um lote de SQL, e você poderá descartar apenas um banco de dados de cada vez.
  
### [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
 Você deve estar conectado ao banco de dados mestre para descartar um banco de dados.
  
 A instrução DROP DATABASE deve ser a única instrução em um lote de SQL, e você poderá descartar apenas um banco de dados de cada vez.

## <a name="permissions"></a>Permissões  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Requer o **controle** no banco de dados, ou **ALTER ANY DATABASE** permissão ou associação no **db_owner** função fixa de banco de dados.  
  
### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 Somente o logon principal no nível de servidor (criado pelo processo de provisionamento) ou membros do **dbmanager** função de banco de dados pode descartar um banco de dados.  
  
### [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Requer o **controle** no banco de dados, ou **ALTER ANY DATABASE** permissão ou associação no **db_owner** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-a-single-database"></a>A. Removendo um único banco de dados  
 O exemplo a seguir remove o nome do banco de dados `Sales`:  
  
```  
DROP DATABASE Sales;  
```  
  
### <a name="b-dropping-multiple-databases"></a>B. Removendo vários bancos de dados  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O exemplo a seguir remove cada um dos bancos de dados listados.  
  
```  
DROP DATABASE Sales, NewSales;  
```  
  
### <a name="c-dropping-a-database-snapshot"></a>C. Removendo um instantâneo de banco de dados  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O exemplo a seguir remove um instantâneo do banco de dados denominado `sales_snapshot0600`, sem afetar o banco de dados de origem.  
  
```  
DROP DATABASE sales_snapshot0600;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  
