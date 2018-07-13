---
title: LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 626b73d3-a257-4b45-82fb-c6299faa0001
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 03d16e57053f1793de0ef878120253cc3a8d0376
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429605"
---
# <a name="localdberrorcannotcreateinstancefolder"></a>LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER
    
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
  
