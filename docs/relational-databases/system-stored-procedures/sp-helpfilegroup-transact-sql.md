---
title: sp_helpfilegroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfilegroup_TSQL
- sp_helpfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfilegroup
ms.assetid: 619716b5-95dc-4538-82ae-4b90b9da8ebc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6fe9798b6a9f560621eba9806e25081f72e316c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68122541"
---
# <a name="sp_helpfilegroup-transact-sql"></a>sp_helpfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os nomes e os atributos de grupos de arquivos associados ao banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpfilegroup [ [ @filegroupname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @filegroupname = ] 'name'`É o nome lógico de qualquer grupo de arquivos no banco de dados atual. o *nome* é **sysname**, com um padrão de NULL. Se o *nome* não for especificado, todos os grupos de itens no banco de dados atual serão listados e somente o primeiro conjunto de resultados mostrado na seção conjuntos de resultados será exibido.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**GroupName**|**sysname**|Nome do grupo de arquivos.|  
|**GroupId**|**smallint**|Identificador de grupo de arquivos numérico.|  
|**FileCount**|**int**|Número de arquivos no grupo de arquivos.|  
  
 Se *Name* for especificado, uma linha para cada arquivo no grupo de arquivos será retornada.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**file_in_group**|**sysname**|Nome lógico do arquivo no grupo de arquivos.|  
|**FileID**|**smallint**|Identificador de arquivos numérico.|  
|**nome do arquivo**|**nchar (260)**|O nome  físico do arquivo que inclui o caminho de diretório.|  
|**tamanho**|**nvarchar (15)**|Tamanho do arquivo em kilobytes.|  
|**MaxSize**|**nvarchar (15)**|Tamanho máximo do arquivo.<br /><br /> É o tamanho máximo até o qual o arquivo pode crescer. Um valor UNLIMITED neste campo indica que o arquivo cresce até o disco ficar cheio.|  
|**growth**|**nvarchar (15)**|Incremento de crescimento do arquivo. Isso indica a quantidade de espaço adicionada ao arquivo toda vez que um novo espaço é necessário.<br /><br /> 0 = Arquivo tem um tamanho fixo e não crescerá.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-all-filegroups-in-a-database"></a>a. Retornando todos os grupos de arquivos de um banco de dados  
 O exemplo a seguir retorna informações sobre os grupos de arquivos no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup;  
GO  
```  
  
### <a name="b-returning-all-files-in-a-filegroup"></a>B. Retornando todos os arquivos de um grupo de arquivos  
 O exemplo a seguir retorna informações para todos os arquivos no grupo de arquivos `PRIMARY` do banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup 'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpfile](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sys. database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys. master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [os grupos de sys. File&#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
