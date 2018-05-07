---
title: sysdatabases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9a19ff47d576a7a2ffe5a72f609a27d5c1214f70
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="syssysdatabases-transact-sql"></a>sys.sysdatabases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada banco de dados em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado pela primeira vez, **sysdatabases** contém entradas para o **mestre**, **modelo**, **msdb**e **tempdb** bancos de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados|  
|**dbid**|**smallint**|ID do banco de dados|  
|**sid**|**varbinary(85)**|ID de sistema do designer do banco de dados|  
|**Modo**|**smallint**|Usado internamente para bloquear um banco de dados enquanto ele é criado.|  
|**status**|**Int**|Bits de status, alguns dos quais podem ser definidos usando [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) conforme observado:<br /><br /> 1 = **autoclose** (ALTER DATABASE)<br /><br /> 4 = **no / bulkcopy** (ALTER DATABASE usando SET RECOVERY)<br /><br /> 8 = **trunc. log no ponto de verificação** (ALTER DATABASE usando SET RECOVERY)<br /><br /> 16 = **interrompida a detecção de página** (ALTER DATABASE)<br /><br /> 32 = **carregar**<br /><br /> 64 = **pré-recuperação**<br /><br /> 128 = **recovering**<br /><br /> 256 = **não recuperado**<br /><br /> 512 = **offline** (ALTER DATABASE)<br /><br /> 1024 = **somente leitura** (ALTER DATABASE)<br /><br /> 2048 = **uso apenas do dbo** (ALTER DATABASE usando SET RESTRICTED_USER)<br /><br /> 4096 = **usuário único** (ALTER DATABASE)<br /><br /> 32768 = **modo de emergência**<br /><br /> 65536 = **SOMA DE VERIFICAÇÃO** (ALTER DATABASE)<br /><br /> 4194304 = **autoshrink** (ALTER DATABASE)<br /><br /> 1073741824 = **desligar corretamente**<br /><br /> Vários bits podem ser ON ao mesmo tempo.|  
|**status2**|**Int**|16384 = **padrão ANSI null** (ALTER DATABASE)<br /><br /> 65536 = **concatenar nulo produz nulo** (ALTER DATABASE)<br /><br /> 131072 = **gatilhos recursivos** (ALTER DATABASE)<br /><br /> 1048576 = **padronizar para cursor local** (ALTER DATABASE)<br /><br /> 8388608 = **identificador entre aspas** (ALTER DATABASE)<br /><br /> 33554432 = **fechar cursor na confirmação** (ALTER DATABASE)<br /><br /> 67108864 = **nulos ANSI** (ALTER DATABASE)<br /><br /> 268435456 = **avisos ANSI** (ALTER DATABASE)<br /><br /> 536870912 = **habilitado de texto completo** (definido por meio de **sp_fulltext_database**)|  
|**crdate**|**datetime**|Data de criação|  
|**reserved**|**datetime**|Reservado para uso futuro.|  
|**category**|**Int**|Contém um bitmap de informações usado para replicação:<br /><br /> 1 = Publicado para replicação de instantâneo ou transacional.<br /><br /> 2 = Assinado para uma publicação de instantâneo ou transacional.<br /><br /> 4 = Publicado para replicação de mesclagem.<br /><br /> 8 = Assinado para uma publicação de mesclagem.<br /><br /> 16 = Banco de dados de distribuição.|  
|**cmptlevel**|**tinyint**|Nível de compatibilidade do banco de dados. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).|  
|**filename**|**nvarchar(260)**|Caminho e nome do sistema operacional para o arquivo primário do banco de dados.<br /><br /> **nome de arquivo** é visível para **dbcreator**, **sysadmin**, o proprietário do banco de dados com permissões CREATE ANY DATABASE ou aos que possuírem qualquer uma das seguintes permissões: ALTER ANY DATABASE CRIAR QUALQUER BANCO DE DADOS, EXIBIR QUALQUER DEFINIÇÃO. Para retornar o caminho e nome de arquivo, consulte o [Sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md) exibição de compatibilidade, ou o [sys. database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) exibição.|  
|**version**|**smallint**|Número de versão interno do código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com que o banco de dados foi criado. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
