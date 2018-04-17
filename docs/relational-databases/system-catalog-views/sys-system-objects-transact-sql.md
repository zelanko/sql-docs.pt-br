---
title: system_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.system_objects
- system_objects
- system_objects_TSQL
- sys.system_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_objects catalog view
ms.assetid: 069e9045-97f2-4463-8e8f-c73855f3ea0a
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 59dbc0db32648c7524b8db3d8f3fd58c48a1421c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="syssystemobjects-transact-sql"></a>sys.system_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para todos os objetos de sistema no escopo do esquema inclusos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Todos os objetos de sistema estão contidos nos esquemas chamados sys ou INFORMATION_SCHEMA.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|nome|**sysname**|Nome do objeto.|  
|object_id|**Int**|Número de identificação do objeto. É exclusivo em um banco de dados.|  
|principal_id|**Int**|ID do proprietário individual, se diferente do proprietário do esquema. Por padrão, os objetos contidos no esquema pertencem ao proprietário do esquema. Porém, outro proprietário pode ser especificado usando a instrução ALTER AUTHORIZATION para alterar a propriedade.<br /><br /> Será NULL se não houver nenhum outro proprietário individual.<br /><br /> Será NULL se o tipo de objeto for um dos seguintes:<br /><br /> C = Restrição CHECK<br /><br /> D = DEFAULT (restrição ou autônomo)<br /><br /> F = Restrição FOREIGN KEY<br /><br /> PK = Restrição PRIMARY KEY<br /><br /> R = Regra (estilo antigo, autônomo)<br /><br /> TA = Gatilho (CLR) de assembly<br /><br /> TR = Gatilho SQL<br /><br /> UQ = Restrição UNIQUE|  
|schema_id|**Int**|ID do esquema em que o objeto está contido.<br /><br /> Para todos os objetos de sistema no escopo do esquema inclusos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse valor estará sempre em (schema_id('sys'), schema_id ('INFORMATION_SCHEMA'))|  
|parent_object_id|**Int**|ID do objeto ao qual este objeto pertence.<br /><br /> 0 = Não é um objeto filho.|  
|Tipo|**char(2)**|Tipo de objeto:<br /><br /> AF = Função de agregação (CLR)<br /><br /> C = Restrição CHECK<br /><br /> D = DEFAULT (restrição ou autônomo)<br /><br /> F = Restrição FOREIGN KEY<br /><br /> FN = Função escalar SQL<br /><br /> FS = Função escalar de assembly (CLR)<br /><br /> FT = Função avaliada por tabela de assembly (CLR)<br /><br /> IF = Função SQL com valor de tabela embutida<br /><br /> IT = tabela interna<br /><br /> P = Procedimento armazenado SQL<br /><br /> PC = procedimento armazenado de Assembly (CLR)<br /><br /> PG = Guia de plano<br /><br /> PK = Restrição PRIMARY KEY<br /><br /> R = Regra (estilo antigo, autônomo)<br /><br /> RF = Procedimento de filtro de replicação<br /><br /> S = Tabela base do sistema<br /><br /> SN = Sinônimo<br /><br /> SQ = Fila de serviço<br /><br /> TA = Gatilho DML de assembly (CLR)<br /><br /> TF = Função com valor de tabela SQL<br /><br /> TR = Gatilho DML de SQL<br /><br /> TT = Tipo de tabela<br /><br /> U = Tabela (definida pelo usuário)<br /><br /> UQ = Restrição UNIQUE<br /><br /> V = Exibição<br /><br /> X = Procedimento armazenado estendido|  
|type_desc|**nvarchar(60)**|Descrição do tipo de objeto. AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> DEFAULT_CONSTRAINT<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> INTERNAL_TABLE<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> RULE<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> SYSTEM_TABLE<br /><br /> SYNONYM<br /><br /> SERVICE_QUEUE<br /><br /> CLR_TRIGGER<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> TABLE_TYPE<br /><br /> USER_TABLE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> VIEW<br /><br /> EXTENDED_STORED_PROCEDURE|  
|create_date|**datetime**|A data em que o objeto foi criado.|  
|modify_date|**datetime**|A data em que o objeto foi modificado pela última vez com uma instrução ALTER. Se o objeto for uma tabela ou uma exibição, modify_date também será alterado quando um índice clusterizado na tabela ou na exibição for criado ou alterado.|  
|is_ms_shipped|**bit**|Objeto é criado por um interno [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componente.|  
|is_published|**bit**|O objeto é publicado.|  
|is_schema_published|**bit**|Apenas o esquema do objeto é publicado.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições do catálogo de objeto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
