---
title: catalog.executables | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: bae22d0c-e190-426f-a074-c1d1170e8dd8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 495a60de43826e633ee6c8eb2bcc7d38cf07706b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912612"
---
# <a name="catalogexecutables"></a>catalog.executables 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta exibição mostra uma linha para cada executável na execução especificada.  
  
 Um executável é uma tarefa ou um contêiner que você adiciona ao fluxo de controle de um pacote.  
  
|Nome da coluna|**Data type**|DESCRIÇÃO|  
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
  
## <a name="remarks"></a>Comentários  
  
