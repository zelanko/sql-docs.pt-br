---
title: sys. Triggers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e2110ba25cf28c344f7e48c9bf8066d1b11381bd
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831298"
---
# <a name="systriggers-transact-sql"></a>sys.triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada objeto que é um gatilho, com um tipo de TR ou TA. Os nomes de gatilho DML têm escopo de esquema e, portanto, são visíveis em **Sys. Objects**. Os nomes dos gatilhos DDL seguem o escopo da entidade pai e são visíveis somente nessa exibição.  
  
 As colunas **parent_class** e **Name** identificam exclusivamente o gatilho no banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do gatilho. Os nomes dos gatilhos DML seguem o escopo do esquema. Os nomes dos gatilhos DDL seguem o escopo com respeito à entidade pai.|  
|**object_id**|**int**|Número de identificação do objeto. É exclusivo em um banco de dados.|  
|**parent_class**|**tinyint**|Classe do pai do gatilho.<br /><br /> 0 = Banco de dados, para os gatilhos DDL.<br /><br /> 1 = Objeto ou coluna para os gatilhos DML.|  
|**parent_class_desc**|**nvarchar(60)**|Descrição da classe pai do gatilho.<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|ID da classe pai do gatilho, conforme segue:<br /><br /> 0 = Gatilhos gerados pelo banco de dados.<br /><br /> Para gatilhos DML, essa é a **object_id** da tabela ou exibição na qual o gatilho DML é definido.|  
|**tipo**|**char(2)**|Tipo de objeto:<br /><br /> TA = Gatilho (CLR) de assembly<br /><br /> TR = Gatilho SQL|  
|**type_desc**|**nvarchar(60)**|Descrição do tipo de objeto.<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|A data em que o gatilho foi criado.|  
|**modify_date**|**datetime**|A data em que o objeto foi modificado pela última vez com uma instrução ALTER.|  
|**is_ms_shipped**|**bit**|O gatilho criado em nome do usuário por um componente interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_disabled**|**bit**|O gatilho está desabilitado.|  
|**is_not_for_replication**|**bit**|O gatilho foi criado como NOT FOR REPLICATION.|  
|**is_instead_of_trigger**|**bit**|1 = Gatilhos INSTEAD OF<br /><br /> 0 = Gatilhos AFTER.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
