---
title: sys. soap_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- soap_endpoints_TSQL
- sys.soap_endpoints
- soap_endpoints
- sys.soap_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.soap_endpoints catalog view
ms.assetid: f50dcbfc-02ed-4a19-9c07-c78a5a1b3224
author: stevestein
ms.author: sstein
ms.openlocfilehash: f7081d96d996d33bbabedd13201d7b0fa2547563
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078670"
---
# <a name="syssoap_endpoints-transact-sql"></a>sys.soap_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Contém uma linha para cada ponto de extremidade no servidor que transmite uma carga útil do tipo SOAP. Para cada linha nessa exibição, há uma linha correspondente com o mesmo **endpoint_id** na exibição de catálogo **Sys. http_endpoints** que transporta os metadados de configuração http.  
  
 
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**< colunas herdadas>**||Para obter uma lista de colunas que essa exibição herda, consulte os [pontos de extremidade &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_sql_language_enabled**|**bit**|1 = A opção BATCHES = ENABLED foi especificada, o que significa que são permitidos lotes SQL ad hoc no ponto de extremidade.|  
|**wsdl_generator_procedure**|**nvarchar (776)**|O nome de três partes do procedimento armazenado que implementa esse método.<br /><br /> Os nomes de métodos exigem sintaxe de três partes rígida. nomes de uma, duas ou quatro partes não são permitidos.|  
|**default_database**|**sysname**|O nome do banco de dados padrão especificado na opção DATABASE =.<br /><br /> NULL = DEFAULT foi especificado.|  
|**default_namespace**|**nvarchar (384)**|O namespace padrão especificado na opção NAMESPACE = ou `https://tempuri.org` , se o padrão foi especificado, em vez disso.|  
|**default_result_schema**|**tinyint**|O valor padrão da opção SCHEMA =.<br /><br /> 0 = NONE<br /><br /> 1 = STANDARD|  
|**default_result_schema_desc**|**nvarchar (60)**|Descrição do valor padrão da opção SCHEMA =.<br /><br /> Nenhuma<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|0 = A opção CHARACTER_SET = SQL foi especificada.<br /><br /> 1 = A opção CHARACTER_SET = XML foi especificada.|  
|**is_session_enabled**|**bit**|0 = A opção SESSION = DISABLE foi especificada.<br /><br /> 1 = A opção SESSION = ENABLED foi especificada.|  
|**session_timeout**|**int**|Valor especificado na opção SESSION_TIMEOUT =.|  
|**login_type**|**nvarchar (60)**|Tipo de autenticação permitido nesse ponto de extremidade.<br /><br /> WINDOWS<br /><br /> MIXED|  
|**header_limit**|**int**|Tamanho máximo permitido para o cabeçalho de SOAP.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]Para obter mais informações, consulte [configuração de visibilidade de metadados](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de pontos de extremidade &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
