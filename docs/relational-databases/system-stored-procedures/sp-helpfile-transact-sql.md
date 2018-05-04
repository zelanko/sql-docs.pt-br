---
title: sp_helpfile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpfile
- sp_helpfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: dc7dde2cbd3ec6b3361785b7d9f02931f812b730
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpfile-transact-sql"></a>sp_helpfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os nomes físicos e os atributos de arquivos associados ao banco de dados atual. Use este procedimento armazenado para determinar os nomes de arquivos a serem anexados ou desanexados do servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@filename =** ] **'***nome***'**  
 É o nome lógico de qualquer arquivo no banco de dados atual. *nome* é **sysname**, com um padrão NULL. Se *nome* não é especificado, os atributos de todos os arquivos de banco de dados atual serão retornados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do arquivo lógico.|  
|**fileid**|**smallint**|Identificador numérico do arquivo. Não é retornada se *nome* especificado *.*|  
|**filename**|**nchar(260)**|Nome do arquivo físico.|  
|**filegroup**|**sysname**|Grupo de arquivos ao qual o arquivo pertence.<br /><br /> NULL = Ele é um arquivo de log. Ele nunca faz parte de um grupo de arquivos.|  
|**size**|**nvarchar(15)**|Tamanho do arquivo em kilobytes.|  
|**MaxSize**|**nvarchar(15)**|Tamanho máximo até o qual o arquivo pode crescer. Um valor UNLIMITED neste campo indica que o arquivo cresce até o disco ficar cheio.|  
|**growth**|**nvarchar(15)**|Incremento de crescimento do arquivo. Ele indica a quantidade de espaço adicionada ao arquivo sempre que um novo espaço é necessário.<br /><br /> 0 = Arquivo tem um tamanho fixo e não crescerá.|  
|**Uso**|**varchar (9)**|Arquivo de dados, o valor é **'dados'** e para o arquivo de log é o valor **'log apenas'**.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre os arquivos no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfile;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
