---
title: sys. dm_db_objects_impacted_on_version_change
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_objects_impacted_on_version_change_TSQL
- dm_db_objects_impacted_on_version_change
- dm_db_objects_impacted_on_version_change_TSQL
- sys.dm_db_objects_impacted_on_version_change
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_objects_impacted_on_version_change
- sys.dm_db_objects_impacted_on_version_change
ms.assetid: b94af834-c4f6-4a27-80a6-e8e71fa8793a
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 0255f7260044ee5c09d020f3ba6310d24bc8cb74
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843858"
---
# <a name="sysdm_db_objects_impacted_on_version_change-azure-sql-database"></a>sys.dm_db_objects_impacted_on_version_change (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Esta exibição do sistema com escopo no banco de dados é criada para fornecer um sistema de alerta rápido para determinar os objetos que serão afetados por uma atualização de versão principal no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Você pode usar a exibição antes ou depois da atualização para obter uma descrição completa dos objetos afetados. Você precisará consultar essa exibição em cada banco de dados para obter uma contabilidade completa no servidor inteiro.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|class|**int** NÃO NULO|A classe do objeto que será afetado:<br /><br /> **1** = restrição<br /><br /> **7** = índices e heaps|  
|class_desc|**nvarchar (60)** NÃO NULO|Descrição da classe:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **INDEX**|  
|major_id|**int** NÃO NULO|ID de objeto da restrição ou ID de objeto da tabela que contém índice ou heap.|  
|minor_id|**int** NULO|**NULL** para restrições<br /><br /> Index_id para índices e heaps|  
|dependência|**nvarchar (60)** NÃO NULO|Descrição da dependência que está causando efeito na restrição ou índice. O mesmo valor é usado também para os avisos gerados durante a atualização.<br /><br /> Exemplos:<br /><br /> **espaço** (para intrínseco)<br /><br /> **Geometry** (para System UDT)<br /><br /> **geografia::P grosseira** (para o método UDT do sistema)|  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão VIEW DATABASE STATE.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma consulta em **Sys. dm_db_objects_impacted_on_version_change** para localizar os objetos afetados por uma atualização para a próxima versão principal do servidor  
  
```  
SELECT * FROM sys.dm_db_objects_disabled_on_version_change;  
GO  
```  
  
```  
class  class_desc        major_id    minor_id    dependency                       
------ ----------------- ----------- ----------- ----------   
1      OBJECT_OR_COLUMN  181575685   NULL        geometry                        
7      INDEX             37575172    1           geometry                        
7      INDEX             2121058592  1           geometry                        
1      OBJECT_OR_COLUMN  101575400   NULL        geometry     
```  
  
## <a name="remarks"></a>Comentários  
  
### <a name="how-to-update-impacted-objects"></a>Como atualizar objetos afetados  
 As etapas ordenadas a seguir descrevem a ação corretiva a ser realizada depois da atualização da próxima versão do serviço de junho.  
  
|Order|Objeto afetado|Ação corretiva|  
|-----------|---------------------|-----------------------|  
|1|**Índices**|Reconstrua qualquer índice identificado por **Sys. dm_db_objects_impacted_on_version_change** por exemplo: `ALTER INDEX ALL ON <table> REBUILD`<br />ou<br />`ALTER TABLE <table> REBUILD`|  
|2|**Objeto**|Todas as restrições identificadas por **Sys. dm_db_objects_impacted_on_version_change** devem ser revalidadas depois que os dados geometry e geography na tabela subjacente são recomputados. Para restrições, revalide usando ALTER TABLE. <br />Por exemplo: <br />`ALTER TABLE <tab> WITH CHECK CHECK CONSTRAINT <constraint name>`<br />ou<br />`ALTER TABLE <tab> WITH CHECK CONSTRAINT ALL`|  
  
  
