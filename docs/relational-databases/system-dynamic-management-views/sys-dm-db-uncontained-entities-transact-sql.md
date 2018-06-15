---
title: sys.dm_db_uncontained_entities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_uncontained_entities
- dm_db_uncontained_entities_TSQL
- sys.dm_db_uncontained_entities_TSQL
- dm_db_uncontained_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_uncontained_entities dynamic management view
ms.assetid: f417efd4-8c71-4f81-bc9c-af13bb4b88ad
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 18f89d3a275a36d32d72524a1c2e650a9e2dc663
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34463892"
---
# <a name="sysdmdbuncontainedentities-transact-sql"></a>sys.dm_db_uncontained_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Mostra qualquer objeto não contido usado no banco de dados. Os objetos não contidos são aqueles que cruzam o limite de banco de dados em um banco de dados independente. Essa exibição pode ser acessada de um banco de dados independente e de um banco de dados dependente. Se sys.DM db_uncontained_entities estiver vazia, o banco de dados não usa nenhuma entidade não contida.  
  
 Se um módulo cruzar o limite de banco de dados mais de uma vez, apenas o primeiro cruzamento descoberto será relatado.  
  
||||  
|-|-|-|  
|**Nome da coluna**|**Tipo**|**Descrição**|  
|*class*|**Int**|1 = Objeto ou coluna (inclui módulos, XPs, exibições, sinônimos e tabelas).<br /><br /> 4 = Entidade do Banco de Dados<br /><br /> 5 = Assembly<br /><br /> 6 = Tipo<br /><br /> 7 = Índice (Índice de Texto Completo)<br /><br /> 12 = Gatilho DDL do Banco de Dados<br /><br /> 19 = Rota<br /><br /> 30 = Especificação de Auditoria|  
|*class_desc*|**nvarchar(120)**|Descrição da classe da entidade. Um dos procedimentos a seguir para corresponder à classe:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **DATABASE_PRINCIPAL**<br /><br /> **ASSEMBLY**<br /><br /> **TYPE**<br /><br /> **INDEX**<br /><br /> **DATABASE_DDL_TRIGGER**<br /><br /> **ROUTE**<br /><br /> **AUDIT_SPECIFICATION**|  
|*major_id*|**Int**|ID da entidade.<br /><br /> Se *classe* = 1, então o object_id<br /><br /> Se *classe* = 4 e, em seguida, principal_id.<br /><br /> Se *classe* = 5 e, em seguida, assembly_id.<br /><br /> Se *classe* = 6 e, em seguida, user_type_id.<br /><br /> Se *classe* = 7, em seguida, index_id.<br /><br /> Se *classe* = 12, em seguida, sys.<br /><br /> Se *classe* = 19, route_id.<br /><br /> Se *classe* = 30 e, em seguida, sys. database_audit_specifications.databse_specification_id.|  
|*statement_line_number*|**Int**|Se a classe for um módulo, retornará o número da linha no qual o uso não contido está localizado.  Caso contrário, o valor será nulo.|  
|*statement_ offset_begin*|**Int**|Se a classe for um módulo, indicará, em bytes, começando com 0, a posição inicial onde uso não contido começa. Caso contrário, o valor de retorno será nulo.|  
|*statement_ offset_end*|**Int**|Se a classe for um módulo, indicará, em bytes, começando com 0, a posição final do uso não contido. Um valor de -1 indica o fim do módulo. Caso contrário, o valor de retorno será nulo.|  
|*statement_type*|**nvarchar(512)**|O tipo de instrução.|  
|*nome de feature_*|**nvarchar(256)**|Retorna o nome externo do objeto.|  
|*feature_type_name*|**nvarchar(256)**|Retorna o tipo de recurso.|  
  
## <a name="remarks"></a>Remarks  
 sys.DM db_uncontained_entities mostra essas entidades que podem, potencialmente, cruzar o limite de banco de dados. Retornará qualquer entidade de usuário que tenha o potencial para usar objetos fora do modelo de banco de dados.  
  
 Os tipos de recurso a seguir são relatados.  
  
-   Comportamento de retenção desconhecido (SQL dinâmico ou resolução de nome adiada)  
  
-   Comando DBCC  
  
-   Procedimento armazenado do sistema  
  
-   Função escalar do sistema  
  
-   Função com valor de tabela do sistema  
  
-   Função interna do sistema  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 sys.DM db_uncontained_entities retorna apenas os objetos para os quais o usuário tem algum tipo de permissão. Para avaliar completamente a contenção do banco de dados, essa função deve ser usada por um usuário com altos privilégios, como um membro do **sysadmin** função de servidor fixa ou **db_owner** função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um procedimento denominado P1 e consulta `sys.dm_db_uncontained_entities`. A consulta relata que P1 usa **sys.endpoints** , que está fora do banco de dados.  
  
```sql  
CREATE DATABASE Test;  
GO  
  
USE Test;  
GO  
CREATE PROC P1  
AS   
SELECT * FROM sys.endpoints ;  
GO  
SELECT SO.name, UE.* FROM sys.dm_db_uncontained_entities AS UE  
LEFT JOIN sys.objects AS SO  
    ON UE.major_id = SO.object_id;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)  
  
  
