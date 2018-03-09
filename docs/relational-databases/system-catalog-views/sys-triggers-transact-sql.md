---
title: sys. Triggers (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- triggers
- triggers_TSQL
- sys.triggers
- sys.triggers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.triggers catalog view
ms.assetid: cefa4fc4-b8b9-4cd7-b124-eed5283acbfc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab5788614af71fe9fa4cab1a4f22e81d5a19a6d8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="systriggers-transact-sql"></a>sys.triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada objeto que é um gatilho, com um tipo de TR ou TA. Os nomes dos gatilhos DML seguem o escopo do esquema e, portanto, são visíveis no **sys. Objects**. Os nomes dos gatilhos DDL seguem o escopo da entidade pai e são visíveis somente nessa exibição.  
  
 O **parent_class** e **nome** colunas identificam exclusivamente o gatilho no banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do gatilho. Os nomes dos gatilhos DML seguem o escopo do esquema. Os nomes dos gatilhos DDL seguem o escopo com respeito à entidade pai.|  
|**object_id**|**int**|Número de identificação do objeto. É exclusivo em um banco de dados.|  
|**parent_class**|**tinyint**|Classe do pai do gatilho.<br /><br /> 0 = Banco de dados, para os gatilhos DDL.<br /><br /> 1 = Objeto ou coluna para os gatilhos DML.|  
|**parent_class_desc**|**nvarchar (60)**|Descrição da classe pai do gatilho.<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|ID da classe pai do gatilho, conforme segue:<br /><br /> 0 = Gatilhos gerados pelo banco de dados.<br /><br /> Gatilhos DML, este é o **object_id** da tabela ou exibição na qual o gatilho DML é definido.|  
|**tipo**|**char(2)**|Tipo de objeto:<br /><br /> TA = Gatilho (CLR) de assembly<br /><br /> TR = Gatilho SQL|  
|**type_desc**|**nvarchar (60)**|Descrição do tipo de objeto.<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|A data em que o gatilho foi criado.|  
|**modify_date**|**datetime**|A data em que o objeto foi modificado pela última vez com uma instrução ALTER.|  
|**is_ms_shipped**|**bit**|O gatilho criado em nome do usuário por um componente interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_disabled**|**bit**|O gatilho está desabilitado.|  
|**is_not_for_replication**|**bit**|O gatilho foi criado como NOT FOR REPLICATION.|  
|**is_instead_of_trigger**|**bit**|1 = Gatilhos INSTEAD OF<br /><br /> 0 = Gatilhos AFTER.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
