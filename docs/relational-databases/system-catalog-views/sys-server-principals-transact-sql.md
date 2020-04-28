---
title: sys. server_principals (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_principals
- sys.server_principals_TSQL
- sys.server_principals
- server_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_principals catalog view
ms.assetid: c5dbe0d8-a1c8-4dc4-b9b1-22af20effd37
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 408ad309ade858c800b79ee83993fda4fe78467a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68133092"
---
# <a name="sysserver_principals-transact-sql"></a>sys.server_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Contém uma linha para cada principal do nível de servidor.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do principal. É exclusivo em um servidor.|  
|**principal_id**|**int**|Número da ID do principal. É exclusivo em um servidor.|  
|**SIDs**|**varbinary (85)**|SID (ID de segurança) do principal. Se for o principal do Windows, corresponde à SID do Windows.|  
|**type**|**Char (1)**|Tipo do principal:<br /><br /> S = Logon SQL<br /><br /> U = Logon do Windows<br /><br /> G = Grupo do Windows<br /><br /> R = Função do servidor<br /><br /> C = Logon mapeado para um certificado<br /><br /> K = Logon mapeado para uma chave assimétrica|  
|**type_desc**|**nvarchar(60)**|Descrição do tipo do principal:<br /><br /> SQL_LOGIN<br /><br /> WINDOWS_LOGIN<br /><br /> WINDOWS_GROUP<br /><br /> SERVER_ROLE<br /><br /> CERTIFICATE_MAPPED_LOGIN<br /><br /> ASYMMETRIC_KEY_MAPPED_LOGIN|  
|**is_disabled**|**int**|1 = O logon está desabilitado.|  
|**create_date**|**datetime**|Hora em que o principal foi criado.|  
|**modify_date**|**datetime**|Hora em que a definição do principal foi modificada pela última vez.|  
|**default_database_name**|**sysname**|Banco de dados padrão para este principal.|  
|**default_language_name**|**sysname**|Linguagem padrão deste principal.|  
|**credential_id**|**int**|ID de uma credencial associada a este principal. Se nenhuma credencial for associada a este principal, credential_id será NULL.|  
|**owning_principal_id**|**int**|O **principal_id** do proprietário de uma função de servidor. NULL se a entidade não for uma função de servidor.|  
|**is_fixed_role**|**bit**|Retornará 1 se a entidade de segurança for uma das funções de servidor internas com permissões fixas. Para obter mais informações, veja [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md).|  
  
## <a name="permissions"></a>Permissões  
 Qualquer logon pode ver seu próprio nome de logon, os logons do sistema e as funções de servidor fixas. Ver outros logons requer ALTER ANY LOGIN ou uma permissão no logon. Ver funções de servidor definidas pelo usuário requer ALTER ANY SERVER ROLE ou associação na função.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir lista as permissões concedidas ou negadas explicitamente a entidades de segurança do servidor.  
  
> [!IMPORTANT]  
>  As permissões de funções de servidor fixas (diferentes de públicas) não aparecem em sys. server_permissions. Portanto, entidades de segurança do servidor podem ter permissões adicionais não listadas aqui.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pe.state_desc, pe.permission_name   
FROM sys.server_principals AS pr   
JOIN sys.server_permissions AS pe   
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
  
  
