---
title: endpoint_webmethods (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.endpoint_webmethods_TSQL
- sys.endpoint_webmethods
- endpoint_webmethods_TSQL
- sys.http_soap_methods_TSQL
- endpoint_webmethods
- sys.http_soap_methods
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoint_webmethods catalog view
ms.assetid: 7dad0cf6-eafa-47cf-98cc-75ba8d3c7959
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 10a25b8b0632cbf8b8836f1f59bdcb6ef6652151
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysendpointwebmethods-transact-sql"></a>sys.endpoint_webmethods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Contém uma linha para o método FOR EACH SOAP definido em um ponto de extremidade HTTP com SOAP habilitado. A combinação das colunas endpoint_id e namespace é exclusiva.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|endpoint_id|**Int**|O ID do ponto de extremidade para o qual webmethod está definido.|  
|namespace|**nvarchar(384)**|Namespace do webmethod.|  
|method_alias|**nvarchar(64)**|Alias para o método.<br /><br /> Observação: [!INCLUDE[tsql](../../includes/tsql-md.md)] identificadores permitem caracteres que não são válidos em nomes de método WSDL.<br /><br /> O alias é usado para mapear o nome exposto na descrição de WSDL do ponto de extremidade ao objeto executável [!INCLUDE[tsql](../../includes/tsql-md.md)] subjacente real chamado quando o webmethod é invocado.|  
|object_name|**nvarchar(776)**|O nome de objeto para o qual o webmethod é redirecionado, conforme especificado na opção NAME =. Partes do nome são separadas por um ponto (.) e delimitadas por colchetes, `[``]`.<br /><br /> O nome do objeto deve ser um nome de três partes, conforme especificado na opção de WSDL.|  
|result_schema|**tinyint**|A opção que determina que, se houver, o XSD seja enviado de volta com uma resposta.<br /><br /> 0 = Nenhum<br /><br /> 1 = Padrão<br /><br /> 2 = Padrão|  
|result_schema_desc|**nvarchar(60)**|A descrição da opção que determina que, se houver, o XSD seja enviado de volta com uma resposta.<br /><br /> Nenhuma<br /><br /> STANDARD<br /><br /> DEFAULT|  
|result_format|**tinyint**|Opção que determina como os resultados são formatados na resposta.<br /><br /> 1 = ALL_RESULTS<br /><br /> 2 = ROWSETS_ONLY<br /><br /> 3 = NENHUM|  
|result_format_desc|**nvarchar(60)**|Descrição da opção que determina como os resultados são formatados na resposta.<br /><br /> ALL_RESULTS<br /><br /> ROWSETS_ONLY<br /><br /> Nenhuma|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do catálogo de pontos de extremidade &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
