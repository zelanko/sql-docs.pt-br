---
title: LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 626b73d3-a257-4b45-82fb-c6299faa0001
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 856b7112cc9f569372e11c8caabd091319f5e872
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840804"
---
# <a name="localdberrorcannotcreateinstancefolder"></a>LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|256|  
|Origem do evento|Tempo de execução de banco de dados local do SQL Server 12.0|  
|Componente|API do tempo de execução de banco de dados local|  
|Texto da mensagem|Não é possível criar a pasta para a instância de banco de dados Local em: %%LOCALAPPDATA%%\Microsoft\Microsoft SQL Server Local DB\Instances\\< nome da instância\>.|  
  
## <a name="explanation"></a>Explicação  
 Uma pasta não pode ser criada abaixo de %userprofile%.  
  
## <a name="user-action"></a>Ação do usuário  
  
