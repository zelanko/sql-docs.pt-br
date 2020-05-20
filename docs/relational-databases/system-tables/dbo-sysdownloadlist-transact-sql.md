---
title: dbo. sysdownloadlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdownloadlist
- sysdownloadlist_TSQL
- dbo.sysdownloadlist_TSQL
- sysdownloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sysdownloadlist system table
ms.assetid: 71087a4c-e829-488e-aa7d-a9476e2b4779
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b3b87a32aec99b0b5775e492191683dd1b3b2366
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813650"
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mantém a fila de instruções de download para todos os servidores de destino.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Coluna de identidade que fornece a sequência de inserção natural de linhas.|  
|**source_server**|**sysname**|Nome do servidor de origem.|  
|**operation_code**|**tinyint**|Código de operação para o trabalho:<br /><br /> **1** = ins (inserir)<br /><br /> **2** = UPD (atualização)<br /><br /> **3** = del (excluir)<br /><br /> **4** = iniciar<br /><br /> **5** = parar|  
|**object_type**|**tinyint**|Código de tipo de objeto.|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|Número de identificação do objeto.|  
|**target_server**|**sysname**|Nome do servidor de destino.|  
|**error_message**|**nvarchar(1024)**|Mensagem de erro se o servidor de destino encontrar um erro ao processar a linha em particular.|  
|**date_posted**|**datetime**|Data e hora em que o trabalho foi postado no servidor de destino.|  
|**date_downloaded**|**datetime**|Data e hora em que o trabalho foi baixado pela última vez.|  
|**status**|**tinyint**|Status do trabalho:<br /><br /> **0** = ainda não baixado<br /><br /> **1** = baixado com êxito|  
|**deleted_object_name**|**sysname**|Nome do objeto excluído.|  
  
 <sup>1</sup> a coluna **object_id** pode ser um valor de **-1**, que corresponde a um valor de todos se a coluna **operation_code** for um valor de excluir.  
  
  
