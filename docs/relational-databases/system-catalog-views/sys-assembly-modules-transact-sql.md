---
title: sys. assembly_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.assembly_modules
- sys.assembly_modules_TSQL
- assembly_modules
- assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_modules catalog view
ms.assetid: 5f9e644e-8065-49a2-b53d-db7df98f70d8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ade1adbfeb8292e894ce18db305687c7092707cf
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391442"
---
# <a name="sysassemblymodules-transact-sql"></a>sys.assembly_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Retorna uma linha para cada função, procedimento ou gatilho definido por um assembly CLR (Common Language Runtime). Esta exibição do catálogo mapeia procedimentos armazenados, gatilhos ou funções CLR para sua implementação subjacente. Os objetos do tipo TA, AF, PC, FS e FT possuem um módulo assembly associado. Para localizar a associação entre o objeto e o assembly, você poderá unir esta exibição do catálogo a outras exibições do catálogo. Por exemplo, quando você cria um procedimento armazenado CLR, ele é representado por uma linha em **sys. Objects**, uma linha na **Procedures** (que herda do **sys. Objects**), e uma linha em **sys. assembly_modules**. O próprio procedimento armazenado é representado pelos metadados em **sys. Objects** e **Procedures**. Referências a implementação de CLR subjacente do procedimento são encontradas no **sys. assembly_modules**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Número de identificação do objeto SQL. É exclusivo em um banco de dados.|  
|**assembly_id**|**int**|ID do assembly a partir do qual o módulo foi criado.|  
|**assembly_class**|**sysname**|Nome da classe dentro do assembly que define este módulo.|  
|**assembly_method**|**sysname**|Nome do método dentro de **assembly_class** que define este módulo.<br /><br /> NULL para funções de agregação (AF).|  
|**null_on_null_input**|**bit**|O módulo foi declarado para produzir uma saída NULL para qualquer entrada NULL.|  
|**execute_as_principal_id**|**int**|ID do banco de dados principal no qual a execução de contexto ocorre, conforme especificado pela cláusula EXECUTE AS da função, do procedimento armazenado ou do gatilho CLR.<br /><br /> NULL = EXECUTE AS CALLER. Esse é o padrão.<br /><br /> ID da entidade de banco de dados especificada = EXECUTE AS SELF, EXECUTE AS *user_name*, ou EXECUTE AS *login_name*.<br /><br /> -2 = EXECUTE AS OWNER.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
