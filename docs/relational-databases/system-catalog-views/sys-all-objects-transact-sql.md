---
description: sys.all_objects (Transact-SQL)
title: sys.all_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/20/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.all_objects
- all_objects_TSQL
- all_objects
- sys.all_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_objects catalog view
ms.assetid: 547e4be4-a8e4-48ce-9d8d-37b169985081
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f6900467bd593afd2a6ece290e8ad35611b2720
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484798"
---
# <a name="sysall_objects-transact-sql"></a>sys.all_objects (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Mostra o UNION de todos os objetos definidos pelo usuário no escopo do esquema e os objetos de sistema.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nome do objeto.|  
|object_id|**int**|Número de identificação do objeto. É exclusivo em um banco de dados.|  
|principal_id|**int**|ID do proprietário individual, se diferente do proprietário do esquema. Por padrão, os objetos contidos no esquema pertencem ao proprietário do esquema. Porém, outro proprietário pode ser especificado usando a instrução ALTER AUTHORIZATION para alterar a propriedade.<br /><br /> Será NULL se não houver nenhum proprietário individual alternativo.<br /><br /> Será NULL se o tipo de objeto for um dos seguintes:<br /><br /> C = Restrição CHECK<br /><br /> D = DEFAULT (restrição ou autônomo)<br /><br /> F = Restrição FOREIGN KEY<br /><br /> PK = Restrição PRIMARY KEY<br /><br /> R = Regra (estilo antigo, autônomo)<br /><br /> TA = Gatilho (CLR) de assembly<br /><br /> TR = Gatilho SQL<br /><br /> UQ = Restrição UNIQUE|  
|schema_id|**int**|ID do esquema que contém o objeto.<br /><br /> Para todos os objetos de sistema no escopo do esquema inclusos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse valor estará sempre em (schema_id('sys'), schema_id('INFORMATION_SCHEMA')).|  
|parent_object_id|**int**|ID do objeto ao qual este objeto pertence.<br /><br /> 0 = Não é um objeto filho.|  
|tipo|**char(2)**|Tipo de objeto:<br /><br /> AF = Função de agregação (CLR)<br /><br /> C = Restrição CHECK<br /><br /> D = DEFAULT (restrição ou autônomo)<br /><br /> F = Restrição FOREIGN KEY<br /><br /> FN = Função escalar SQL<br /><br /> FS = Função escalar de assembly (CLR)<br /><br /> FT = Função avaliada por tabela de assembly (CLR)<br /><br /> IF = Função SQL com valor de tabela embutida<br /><br /> TI = tabela interna<br /><br /> P = Procedimento armazenado SQL<br /><br /> PC = assembly (CLR) armazenado-procedimento<br /><br /> PG = Guia de plano<br /><br /> PK = Restrição PRIMARY KEY<br /><br /> R = Regra (estilo antigo, autônomo)<br /><br /> RF = Procedimento de filtro de replicação<br /><br /> S = Tabela base do sistema<br /><br /> SN = Sinônimo<br /><br /> SO = Objeto de sequência<br /><br /> SQ = Fila de serviço<br /><br /> TA = Gatilho DML de assembly (CLR)<br /><br /> TF = Função com valor de tabela SQL<br /><br /> TR = Gatilho DML de SQL<br /><br /> TT = Tipo de tabela<br /><br /> U = Tabela (definida pelo usuário)<br /><br /> UQ = Restrição UNIQUE<br /><br /> V = Exibição<br /><br /> X = Procedimento armazenado estendido|  
|type_desc|**nvarchar(60)**|Descrição do tipo de objeto. AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> DEFAULT_CONSTRAINT<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> INTERNAL_TABLE<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> RULE<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> SYSTEM_TABLE<br /><br /> SYNONYM<br /><br /> SERVICE_QUEUE<br /><br /> CLR_TRIGGER<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> TABLE_TYPE<br /><br /> USER_TABLE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> VIEW<br /><br /> EXTENDED_STORED_PROCEDURE|  
|create_date|**datetime**|A data em que o objeto foi criado.|  
|modify_date|**datetime**|A data em que o objeto foi modificado pela última vez com uma instrução ALTER. Se o objeto for uma tabela ou uma exibição, modify_date também será alterado quando um índice na tabela ou exibição for criado ou modificado.|  
|is_ms_shipped|**bit**|O objeto é criado por um componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interno.|  
|is_published|**bit**|O objeto é publicado.|  
|is_schema_published|**bit**|Apenas o esquema do objeto é publicado.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)  
  
  
