---
title: Catalog. catalog_properties (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca3d5da05126d5b71bf6d714f9e8449f9f5c8335
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcatalogproperties-ssisdb-database"></a>catalog.catalog_properties (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe as propriedades do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|O nome da propriedade do catálogo.|  
|property_value|**nvarchar(256)**|O valor da propriedade do catálogo.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada propriedade do catálogo. As propriedades mostradas por esta exibição incluem o seguinte:  
  
|Nome da propriedade|Description|  
|-------------------|-----------------|  
|**ENCRYPTION_ALGORITHM**|O tipo de algoritmo de criptografia usado para criptografar dados confidenciais. Os valores com suporte incluem: `DES`, `TRIPLE_DES`, `TRIPLE_DES_3KEY`, `DESX`, `AES_128`, `AES_192` e `AES_256`. Observação: o banco de dados do catálogo deve estar em modo de usuário único para alterar essa propriedade.|  
|**MAX_PROJECT_VERSIONS**|O número de novas versões do projeto que serão retidas para um único projeto. Quando a limpeza de versão estiver habilitada, as versões anteriores além desta contagem serão excluídas.|  
|**OPERATION_CLEANUP_ENABLED**|Quando o valor é `TRUE`, detalhes da operação e as mensagens da operação anteriores **RETENTION_WINDOW** (dias) serão excluídos do catálogo. Quando o valor for `FALSE`, todos os detalhes da operação e mensagens da operação serão armazenados no catálogo. Observação: um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa a limpeza da operação.|  
|**RETENTION_WINDOW**|O número de dias em que os detalhes da operação e as mensagens da operação serão armazenados no catálogo. Quando o valor for `-1`, a janela de retenção será infinita. Observação: Se nenhuma limpeza for desejada, defina **OPERATION_CLEANUP_ENABLED** para **FALSE**.|  
|**VALIDATION_TIMEOUT**|As validações serão interrompidas caso não sejam concluídas no número de segundos especificado por esta propriedade.|  
|**VERSION_CLEANUP_ENABLED**|Quando o valor é `TRUE`, somente o **MAX_PROJECT_VERSIONS** número de versões do projeto é armazenado no catálogo e todas as outras versões do projeto serão excluídas. Quando o valor é **FALSE**, todas as versões de projeto são armazenadas no catálogo. Observação: um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa a limpeza da operação.|  
|**SERVER_LOGGING_LEVEL**|O nível de log padrão para o servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
  

