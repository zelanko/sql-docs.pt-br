---
title: sys. sysdatabases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdatabases_TSQL
- sys.sysdatabases_TSQL
- sys.sysdatabases
- sysdatabases
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdatabases compatibility view
- sysdatabases system table
ms.assetid: 60a93880-62f1-4eda-a886-f046706ba90c
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b0dab1ca5f21ced6a54192a4b0173ead68fd6f5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68089161"
---
# <a name="syssysdatabases-transact-sql"></a>sys.sysdatabases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada banco de dados em uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instância do. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o é instalado pela primeira vez, o **sysdatabases** contém entradas para os bancos de dados **mestre**, **modelo**, **msdb**e **tempdb** .  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados|  
|**DBID**|**smallint**|ID do banco de dados|  
|**SIDs**|**varbinary (85)**|ID de sistema do designer do banco de dados|  
|**mode**|**smallint**|Usado internamente para bloquear um banco de dados enquanto ele é criado.|  
|**status**|**int**|Bits de status, alguns dos quais podem ser definidos usando [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) , conforme observado:<br /><br /> 1 = **fechar** novamente (ALTER DATABASE)<br /><br /> 4 = **Select Into/bulkcopy** (ALTER DATABASE usando Set Recovery)<br /><br /> 8 = **trunc. log em chkpt** (ALTER DATABASE usando Set Recovery)<br /><br /> 16 = **detecção de página interrompida** (ALTER DATABASE)<br /><br /> 32 = **carregamento**<br /><br /> 64 = **pré-recuperação**<br /><br /> 128 = **recovering**<br /><br /> 256 = **não recuperado**<br /><br /> 512 = **offline** (ALTER DATABASE)<br /><br /> 1024 = **somente leitura** (ALTER DATABASE)<br /><br /> 2048 = **dbo use only** (ALTER DATABASE usando Set RESTRICTED_USER)<br /><br /> 4096 = **usuário único** (ALTER DATABASE)<br /><br /> 32768 = **modo de emergência**<br /><br /> 65536 = **soma de verificação** (ALTER DATABASE)<br /><br /> 4194304 = **redução** automática (ALTER DATABASE)<br /><br /> 1073741824 = **desligamento limpo**<br /><br /> Vários bits podem ser ON ao mesmo tempo.|  
|**status2**|**int**|16384 = **padrão ANSI NULL** (ALTER DATABASE)<br /><br /> 65536 = **concat NULL produz nulo** (ALTER DATABASE)<br /><br /> 131072 = **gatilhos recursivos** (ALTER DATABASE)<br /><br /> 1048576 = **padrão para o cursor local** (ALTER DATABASE)<br /><br /> 8388608 = **identificador entre aspas** (ALTER DATABASE)<br /><br /> 33554432 = **fechamento do cursor na confirmação** (ALTER DATABASE)<br /><br /> 67108864 = **ANSI NULLS** (ALTER DATABASE)<br /><br /> 268435456 = **avisos ANSI** (ALTER DATABASE)<br /><br /> 536870912 = **texto completo habilitado** (definido usando **sp_fulltext_database**)|  
|**crdate**|**datetime**|Data de criação|  
|**reservado**|**datetime**|Reservado para uso futuro.|  
|**category**|**int**|Contém um bitmap de informações usado para replicação:<br /><br /> 1 = Publicado para replicação de instantâneo ou transacional.<br /><br /> 2 = Assinado para uma publicação de instantâneo ou transacional.<br /><br /> 4 = Publicado para replicação de mesclagem.<br /><br /> 8 = Assinado para uma publicação de mesclagem.<br /><br /> 16 = Banco de dados de distribuição.|  
|**cmptlevel**|**tinyint**|Nível de compatibilidade do banco de dados. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).|  
|**nome do arquivo**|**nvarchar(260)**|Caminho e nome do sistema operacional para o arquivo primário do banco de dados.<br /><br /> o **nome do arquivo** é visível para **dbcreator**, **sysadmin**, o proprietário do banco de dados com permissões para criar qualquer banco de dados ou para os que têm uma das seguintes permissões: alterar qualquer banco de dados, criar qualquer banco de dados, exibir qualquer definição. Para retornar o caminho e o nome do arquivo, consulte a exibição de compatibilidade [Sys. sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md) ou a exibição [Sys. database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) .|  
|**version**|**smallint**|Número de versão interno do código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com que o banco de dados foi criado. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
