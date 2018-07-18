---
title: sys. server_permissions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.server_permissions_TSQL
- sys.server_permissions
- server_permissions
- server_permissions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_permissions catalog view
ms.assetid: 7d78bf17-6c64-4166-bd0b-9e9e20992136
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 16200de0c63979912b893fa84e7b36cf93a4ec62
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38038867"
---
# <a name="sysserverpermissions-transact-sql"></a>sys.server_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Retorna uma linha para cada permissão em nível de servidor.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|Identifica a classe na qual a permissão existe.<br /><br /> 100 = Servidor<br /><br /> 101 = Principal de servidor<br /><br /> 105 = Ponto de extremidade|  
|**class_desc**|**nvarchar(60)**|Descrição de classe na qual a permissão existe. Um dos valores seguintes:<br /><br /> **SERVIDOR**<br /><br /> **SERVER_PRINCIPAL**<br /><br /> **ENDPOINT**|  
|**major_id**|**int**|ID do protegível no qual a permissão existe, interpretada de acordo com a classe. Em geral, é o tipo de ID que se aplica àquilo que a classe representa. A interpretação para sem-padrão é a seguinte:<br /><br /> 100 = sempre 0|  
|**minor_id**|**int**|ID secundária na qual a permissão existe, interpretada de acordo com a classe.|  
|**grantee_principal_id**|**int**|ID do principal de servidor para a qual as permissões são concedidas.|  
|**grantor_principal_id**|**int**|ID do principal de servidor do concessor dessas permissões.|  
|**type**|**char(4)**|Tipo de permissão de servidor. Para obter uma lista de tipos de permissão, consulte a próxima tabela.|  
|**permission_name**|**nvarchar(128)**|Nome de permissão.|  
|**state**|**char(1)**|Estado de permissão:<br /><br /> D = Negar<br /><br /> R = Revogar<br /><br /> G = Conceder<br /><br /> W = opção concessão com concessão|  
|**state_desc**|**nvarchar(60)**|Descrição do estado da permissão:<br /><br /> DENY<br /><br /> REVOKE<br /><br /> GRANT<br /><br /> GRANT_WITH_GRANT_OPTION|  
  
|Tipo de permissão|Nome de permissão|Aplica-se a protegíveis|  
|---------------------|---------------------|--------------------------|  
|ADBO|ADMINISTER BULK OPERATIONS|SERVER|  
|AL|ALTER|ENDPOINT, LOGIN|  
|ALCD|ALTER ANY CREDENTIAL|SERVER|  
|ALCO|ALTER ANY CONNECTION|SERVER|  
|ALDB|ALTER ANY DATABASE|SERVER|  
|ALES|ALTER ANY EVENT NOTIFICATION|SERVER|  
|ALHE|ALTER ANY ENDPOINT|SERVER|  
|ALLG|ALTER ANY LOGIN|SERVER|  
|ALLS|ALTER ANY LINKED SERVER|SERVER|  
|ALRS|ALTER RESOURCES|SERVER|  
|ALSS|ALTER SERVER STATE|SERVER|  
|ALST|ALTER SETTINGS|SERVER|  
|ALTR|ALTER TRACE|SERVER|  
|AUTH|AUTHENTICATE SERVER|SERVER|  
|CL|CONTROL|ENDPOINT, LOGIN|  
|CL|CONTROL SERVER|SERVER|  
|CO|CONNECT|ENDPOINT|  
|COSQ|CONNECT SQL|SERVER|  
|CRDB|CREATE ANY DATABASE|SERVER|  
|CRDE|CREATE DDL EVENT NOTIFICATION|SERVER|  
|CRHE|CREATE ENDPOINT|SERVER|  
|CRTE|CREATE TRACE EVENT NOTIFICATION|SERVER|  
|IM|IMPERSONATE|Logon|  
|SHDN|SHUTDOWN|SERVER|  
|TO|TAKE OWNERSHIP|ENDPOINT|  
|VW|VIEW DEFINITION|ENDPOINT, LOGIN|  
|VWAD|VIEW ANY DEFINITION|SERVER|  
|VWDB|VIEW ANY DATABASE|SERVER|  
|VWSS|VIEW SERVER STATE|SERVER|  
|XA|EXTERNAL ACCESS|SERVER|  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode ver suas próprias permissões. Para ver as permissões de outros logons, requer VIEW DEFINITION, ALTER ANY LOGIN ou qualquer permissão em um logon. Ver funções de servidor definidas pelo usuário requer ALTER ANY SERVER ROLE ou associação na função.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir lista as permissões concedidas ou negadas explicitamente a entidades de segurança do servidor.  
  
> [!IMPORTANT]  
>  As permissões de funções de servidor fixas não aparecem em sys.server_permissions. Portanto, entidades de segurança do servidor podem ter permissões adicionais não listadas aqui.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pe.state_desc, pe.permission_name   
FROM sys.server_principals AS pr   
JOIN sys.server_permissions AS pe   
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
  
  
