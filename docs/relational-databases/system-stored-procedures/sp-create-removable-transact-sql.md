---
title: sp_create_removable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_removable
- sp_create_removable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_removable
ms.assetid: 06e36ae5-f70d-4a26-9a7f-ee4b9360b355
author: stevestein
ms.author: sstein
ms.openlocfilehash: d6f842b96a9b179548688a4c655a566087ba1ebf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108620"
---
# <a name="spcreateremovable-transact-sql"></a>sp_create_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um banco de dados de mídia removível. Cria três ou mais arquivos (um para as tabelas de catálogo de sistema, um para o log de transações e um ou mais para as tabelas de dados) e coloca o banco de dados nesses arquivos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] É recomendável que você use [criar banco de dados](../../t-sql/statements/create-database-sql-server-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_create_removable   
   [ @dbname = ] 'dbname',   
   [ @syslogical= ] 'syslogical',   
   [ @sysphysical = ] 'sysphysical',   
   [ @syssize = ] syssize,   
   [ @loglogical = ] 'loglogical',   
   [ @logphysical = ] 'logphysical',   
   [ @logsize = ] logsize,   
   [ @datalogical1 = ] 'datalogical1',   
   [ @dataphysical1 = ] 'dataphysical1',   
   [ @datasize1 = ] datasize1 ,   
   [ @datalogical16 = ] 'datalogical16',   
   [ @dataphysical16 = ] 'dataphysical16',   
   [ @datasize16 = ] datasize16 ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'` É o nome do banco de dados criado para uso em mídia removível. *DBName* está **sysname**.  
  
`[ @syslogical = ] 'syslogical'` É o nome lógico do arquivo que contém as tabelas de catálogo do sistema. *syslogical* está **sysname**.  
  
`[ @sysphysical = ] 'sysphysical'` É o nome físico. Isso inclui um caminho totalmente qualificado do arquivo que contém as tabelas de catálogo de sistema. *sysphysical* está **nvarchar (260)** .  
  
`[ @syssize = ] syssize` É o tamanho, em megabytes, do arquivo que contém o sistema de tabelas de catálogo. *syssize* está **int**. O mínimo *syssize* é 1.  
  
`[ @loglogical = ] 'loglogical'` É o nome lógico do arquivo que contém o log de transações. *loglogical* está **sysname**.  
  
`[ @logphysical = ] 'logphysical'` É o nome físico. Isso inclui um caminho totalmente qualificado do arquivo que contém o log de transações. *logphysical* está **nvarchar (260)** .  
  
`[ @logsize = ] logsize` É o tamanho, em megabytes, do arquivo que contém o log de transações. *logsize* está **int**. O mínimo *logsize* é 1.  
  
`[ @datalogical1 = ] 'datalogical'` É o nome lógico de um arquivo que contém as tabelas de dados. *datalogical* está **sysname**.  
  
 Deve ser de 1 a 16 arquivos de dados. Geralmente, mais de um arquivo de dados é criado quando é esperado que o banco de dados seja grande e deve ser distribuído em vários discos.  
  
`[ @dataphysical1 = ] 'dataphysical'` É o nome físico. Isso inclui um caminho totalmente qualificado do arquivo que contém as tabelas de dados. *dataphysical* está **nvarchar (260)** .  
  
`[ @datasize1 = ] 'datasize'` É o tamanho, em megabytes, de um arquivo que contém tabelas de dados. *datasize* está **int**. O mínimo *datasize* é 1.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Se você quiser fazer uma cópia de seu banco de dados em mídia removível, como um CD, e distribuir o banco de dados a outros usuários, use este procedimento armazenado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE DATABASE, CREATE ANY DATABASE ou ALTER ANY DATABASE.  
  
 Para manter controle sobre o uso do disco em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a permissão para criar bancos de dados geralmente é limitada a algumas contas de logon.  
  
### <a name="permissions-on-data-and-log-files"></a>Permissões em arquivos de dados e de log  
 Sempre que determinadas operações são executadas em um banco de dados, as permissões correspondentes são definidas nos respectivos arquivos de dados e de log. As permissões evitam que os arquivos sejam violados acidentalmente caso residam em um diretório com permissões abertas.  
  
|Operação no banco de dados|Permissões definidas em arquivos|  
|---------------------------|------------------------------|  
|Modificado para adicionar um novo arquivo|Criado|  
|Incluído em backup|Anexado|  
|Restaurado|Desanexado|  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não define dados e permissões de arquivos de log.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria o banco de dados `inventory` como um banco de dados removível.  
  
```  
EXEC sp_create_removable 'inventory',   
   'invsys',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invsys.mdf'  
, 2,   
   'invlog',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invlog.ldf', 4,  
   'invdata',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invdata.ndf',   
10;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_certify_removable &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-certify-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
