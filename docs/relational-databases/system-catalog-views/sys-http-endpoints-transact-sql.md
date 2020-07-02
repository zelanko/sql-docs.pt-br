---
title: sys. http_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.http_endpoints
- http_endpoints
- sys.http_endpoints_TSQL
- http_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.http_endpoints catalog view
ms.assetid: 16f59695-ecd9-457e-8874-055af63f8ea7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 38697ada64127d3bb9f8e3fc5858cd69f1698f85
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764514"
---
# <a name="syshttp_endpoints-transact-sql"></a>sys.http_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada ponto de extremidade criado no servidor que usa o protocolo HTTP.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**< colunas herdadas>**||Herda colunas de [pontos sys. end&#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**locais**|**nvarchar(128)**|Nome do computador host do site, como especificado na opção SITE =.|  
|**url_path**|**nvarchar(4000)**|Parte apenas do caminho da URL para este ponto de extremidade HTTP, como especificado pela opção PATH=.|  
|**is_clear_port_enabled**|**bit**|1 = Limpar porta é habilitado por meio da opção PORT = CLEAR.|  
|**clear_port**|**int**|Número de porta especificado na opção CLEAR PORT =.<br /><br /> NULL = Não especificado.|  
|**is_ssl_port_enabled**|**bit**|1 = A porta SSL é habilitada por meio da opção PORT = SSL.|  
|**ssl_port**|**int**|Valor de número de porta especificado na opção SSL PORT =.<br /><br /> NULL = Não especificado.|  
|**is_anonymous_enabled**|**bit**|1 = O acesso anônimo é habilitado por meio da opção AUTHENTICATION = ANONYMOUS.|  
|**is_basic_auth_enabled**|**bit**|1 = A autenticação básica é habilitada por meio da opção AUTHENTICATION = BASIC.|  
|**is_digest_auth_enabled**|**bit**|1 = A autenticação Digest é habilitada por meio da opção AUTHENTICATION = DIGEST.|  
|**is_kerberos_auth_enabled**|**bit**|1 = Autenticação integrada habilitada por meio da opção AUTHENTICATION = KERBEROS.|  
|**is_ntlm_auth_enabled**|**bit**|1 = Autenticação integrada habilitada por meio da opção AUTHENTICATION = NTLM.|  
|**is_integrated_auth_enabled**|**bit**|1 = Autenticação integrada habilitada por meio da opção AUTHENTICATION = INTEGRATED.|  
|**authorization_realm**|**nvarchar(128)**|Dica retornada ao cliente como parte do desafio de autenticação HTTP DIGEST. O valor da opção AUTH REALM.<br /><br /> É NULL se não especificado ou se a autenticação DIGEST não estiver habilitada.|  
|**default_logon_domain**|**nvarchar(128)**|Domínio de logon padrão, se você habilitar autenticação BASIC. O valor da opção DEFAULT LOGON DOMAIN.<br /><br /> É NULL se não especificado ou se a autenticação BASIC não estiver habilitada.|  
|**is_compression_enabled**|**bit**|1 = A opção COMPRESSION = ENABLED é definida.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições do catálogo de pontos de extremidade &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
