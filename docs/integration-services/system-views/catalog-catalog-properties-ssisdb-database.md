---
title: catalog.catalog_properties (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/11/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 455bea0ce159382e30dfae98d8d43041c0d16879
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715487"
---
# <a name="catalogcatalogproperties-ssisdb-database"></a>catalog.catalog_properties (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe as propriedades do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|O nome da propriedade do catálogo.|  
|property_value|**nvarchar(256)**|O valor da propriedade do catálogo.|  
  
## <a name="remarks"></a>Remarks  
 Esta exibição mostra uma linha para cada propriedade do catálogo.
  
|Nome da propriedade|Descrição|  
|-------------------|-----------------|  
|**DEFAULT_EXECUTION_MODE**|O modo de execução padrão de todo o servidor para pacotes – `Server` (0) ou `Scale Out` (1). |
|**ENCRYPTION_ALGORITHM**|O tipo de algoritmo de criptografia usado para criptografar dados confidenciais. Os valores com suporte incluem: `DES`, `TRIPLE_DES`, `TRIPLE_DES_3KEY`, `DESX`, `AES_128`, `AES_192` e `AES_256`. Observação: o banco de dados do catálogo precisa estar em modo de usuário único para alterar essa propriedade.|
|**IS_SCALEOUT_ENABLED**|Quando o valor é `True`, o recurso SSIS Scale Out está habilitado. Se você não tiver habilitado o Scale Out, essa propriedade poderá não aparecer na exibição.|
|**MAX_PROJECT_VERSIONS**|O número de novas versões do projeto que são retidas para um único projeto. Quando a limpeza de versão estiver habilitada, as versões anteriores além desta contagem serão excluídas.|  
|**OPERATION_CLEANUP_ENABLED**|Quando o valor for `TRUE`, os detalhes da operação e as mensagens da operação anteriores a **RETENTION_WINDOW** (dias) serão excluídos do catálogo. Quando o valor for `FALSE`, todos os detalhes da operação e mensagens da operação serão armazenados no catálogo. Observação: um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa a limpeza da operação.|  
|**RETENTION_WINDOW**|O número de dias em que os detalhes da operação e as mensagens da operação serão armazenados no catálogo. Quando o valor for `-1`, a janela de retenção será infinita. Observação: Se nenhuma limpeza for desejada, defina **OPERATION_CLEANUP_ENABLED** como **FALSE**.|
|**SCHEMA_BUILD**|O número de build do esquema de banco de dados do catálogo SSISDB. Esse número mudará sempre que o catálogo do SSISDB for criado ou atualizado.|
|**SCHEMA_VERSION**|O número de versão principal do esquema de banco de dados do catálogo SSISDB. Esse número mudará sempre que o catálogo do SSISDB for criado ou o upgrade da versão principal for realizado.|
|**VALIDATION_TIMEOUT**|As validações serão interrompidas caso não sejam concluídas no número de segundos especificado por esta propriedade.|  
|**SERVER_CUSTOMIZED_LOGGING_LEVEL**|O nível de log personalizado padrão para o servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se você não criou nenhum nível de log personalizado, essa propriedade pode não aparecer na exibição.|
|**SERVER_LOGGING_LEVEL**|O nível de log padrão para o servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|
|**SERVER_OPERATION_ENCRYPTION_LEVEL**|Quando o valor é 1 (`PER_EXECUTION`) o certificado e a chave simétrica usados para proteger parâmetros de execução e logs de execução confidenciais são criados para cada *execução*. Quando o valor for 2 (`PER_PROJECT`), o certificado e a chave simétrica são criados uma vez para cada *projeto*. Para obter mais informações sobre essa propriedade, consulte os comentários para o procedimento armazenado [catalog.cleanup_server_log](../system-stored-procedures/catalog-cleanup-server-log.md#remarks) do SSIS.|
|**VERSION_CLEANUP_ENABLED**|Quando o valor for `TRUE`, somente o número **MAX_PROJECT_VERSIONS** de versões do projeto serão armazenadas no catálogo e todas as outras versões do projeto serão excluídas. Quando o valor for **FALSE**, todas as versões do projeto serão armazenadas no catálogo. Observação: um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa a limpeza da operação.|
|||
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
  
