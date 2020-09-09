---
description: sp_helpfile (Transact-SQL)
title: sp_helpfile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfile
- sp_helpfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7bb8c6ff5fe18393db1c08bae888d1479a7f2594
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549631"
---
# <a name="sp_helpfile-transact-sql"></a>sp_helpfile (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna os nomes físicos e os atributos de arquivos associados ao banco de dados atual. Use este procedimento armazenado para determinar os nomes de arquivos a serem anexados ou desanexados do servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @filename = ] 'name'` É o nome lógico de qualquer arquivo no banco de dados atual. o *nome* é **sysname**, com um padrão de NULL. Se o *nome* não for especificado, os atributos de todos os arquivos no banco de dados atual serão retornados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do arquivo lógico.|  
|**FileID**|**smallint**|Identificador numérico do arquivo. Não será retornado se o *nome* for especificado *.*|  
|**nome do arquivo**|**nchar (260)**|Nome do arquivo físico.|  
|**arquivos**|**sysname**|Grupo de arquivos ao qual o arquivo pertence.<br /><br /> NULL = Ele é um arquivo de log. Ele nunca faz parte de um grupo de arquivos.|  
|**size**|**nvarchar (15)**|Tamanho do arquivo em kilobytes.|  
|**MaxSize**|**nvarchar (15)**|Tamanho máximo até o qual o arquivo pode crescer. Um valor UNLIMITED neste campo indica que o arquivo cresce até o disco ficar cheio.|  
|**crescimento**|**nvarchar (15)**|Incremento de crescimento do arquivo. Ele indica a quantidade de espaço adicionada ao arquivo sempre que um novo espaço é necessário.<br /><br /> 0 = Arquivo tem um tamanho fixo e não crescerá.|  
|**usos**|**varchar (9)**|Para o arquivo de dados, o valor é **' somente dados '** e, para o arquivo de log, o valor é **' log only '**.|  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpfilegroup ](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys. master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
