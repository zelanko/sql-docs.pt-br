---
title: catalog.environment_variables (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 45f5aacd-505a-443b-8fc2-c7929e78cff8
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b5578c159f20a0ccbc2fca2811921270d61990da
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406078"
---
# <a name="catalogenvironmentvariables-ssisdb-database"></a>catalog.environment_variables (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os detalhes de variável de ambiente para todos os ambientes no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|variable_id|**bigint**|O ID (identificador exclusivo) da variável de ambiente.|  
|environment_id|**bigint**|O ID exclusivo do ambiente ao qual a variável está associada.|  
|NAME|**sysname**|O nome da variável de ambiente.|  
|descrição|**nvarchar(1024)**|A descrição da variável do ambiente.|  
|Tipo|**nvarchar(128)**|O tipo de dados da variável do ambiente.|  
|sensitive|**bit**|Quando o valor for `1`, a variável será confidencial e criptografada quando for armazenada. Quando o valor for `0`, a variável não será confidencial e o valor será armazenado em texto não criptografado.|  
|value|**sql_variant**|O valor da variável de ambiente. Quando sensitive é `0`, o valor do texto sem formatação é mostrado. Quando sensitive é `1`, o valor **NULL** é exibido.|  
  
## <a name="remarks"></a>Remarks  
 Esta exibição mostra uma linha para cada variável de ambiente no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ no ambiente correspondente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
