---
title: catalog.environment_variables (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 45f5aacd-505a-443b-8fc2-c7929e78cff8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fdb7a7c325a6189feaea690fe2cc22d685ba86e6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296655"
---
# <a name="catalogenvironment_variables-ssisdb-database"></a>catalog.environment_variables (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os detalhes de variável de ambiente para todos os ambientes no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|variable_id|**bigint**|O ID (identificador exclusivo) da variável de ambiente.|  
|environment_id|**bigint**|O ID exclusivo do ambiente ao qual a variável está associada.|  
|name|**sysname**|O nome da variável de ambiente.|  
|descrição|**nvarchar(1024)**|A descrição da variável do ambiente.|  
|type|**nvarchar(128)**|O tipo de dados da variável do ambiente.|  
|sensitive|**bit**|Quando o valor for `1`, a variável será confidencial e criptografada quando for armazenada. Quando o valor for `0`, a variável não será confidencial e o valor será armazenado em texto não criptografado.|  
|value|**sql_variant**|O valor da variável de ambiente. Quando sensitive é `0`, o valor do texto sem formatação é mostrado. Quando sensitive é `1`, o valor **NULL** é exibido.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada variável de ambiente no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ no ambiente correspondente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
