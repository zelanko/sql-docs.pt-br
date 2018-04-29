---
title: catalog.executables | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: bae22d0c-e190-426f-a074-c1d1170e8dd8
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f202b19fcd98967b345afef6a8285192ae04585
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogexecutables"></a>catalog.executables
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta exibição mostra uma linha para cada executável na execução especificada.  
  
 Um executável é uma tarefa ou um contêiner que você adiciona ao fluxo de controle de um pacote.  
  
|Nome da coluna|**Data type**|Description|  
|-----------------|-------------------|-----------------|  
|executable_id|**bigint**|O identificador exclusivo do executável.|  
|execution_id|**bigint**|O identificador exclusivo da instância de execução.|  
|executable_name|**nvarchar(4000)**|O nome do executável.|  
|executable_guid|**nvarchar(38)**|O GUID do executável.|  
|package_name|**nvarchar(260)**|O nome do pacote.|  
|package_path|**nvarchar(max)**|O caminho do pacote.|  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
## <a name="remarks"></a>Remarks  
  
