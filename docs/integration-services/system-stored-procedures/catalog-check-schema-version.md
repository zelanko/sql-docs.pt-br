---
title: catalog.check_schema_version | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d0568db561467e05b73993fe183d0da179fb8d0
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogcheckschemaversion"></a>catalog.check_schema_version
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Determina se o esquema de catálogo SSISDB e os binários [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (ISServerExec e SQLCLR assembly) são compatíveis.  
  
 O ISServerExec.exc registra em log uma mensagem de erro quando o esquema e os binários são incompatíveis.  
  
 A versão do esquema de SSISDB é incrementada quando o esquema é alterado durante a aplicação de patches e durante atualizações. É recomendado que você execute este procedimento armazenado depois que um backup de SSISDB tiver sido restaurado para assegurar que o esquema e os binários sejam compatíveis.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.check_schema_version [@use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @use32bitruntime= ] *use32bitruntime*  
 Quando o parâmetro estiver definido para **True**, a versão de 32 bits de dtexec será chamada. O *use32bitruntime* é **Bool**.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige a seguinte permissão:  
  
-   Associação à função de banco de dados **ssis_admin**.  
  
  
