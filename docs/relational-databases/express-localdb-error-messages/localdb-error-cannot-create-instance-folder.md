---
description: LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER
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
ms.openlocfilehash: d29d8e02729b78814ac7bdb045535953c4b5ced7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88329342"
---
# <a name="localdb_error_cannot_create_instance_folder"></a>LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |
| --------- | ----- |
|Nome do Produto|SQL Server|  
|ID do evento|256|  
|Origem do Evento|Runtime de banco de dados local do SQL Server 12.0|  
|Componente|API do runtime de banco de dados local|  
|Texto da mensagem|Não é possível criar a pasta para a instância do banco de dados local em:%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server local DB\Instances \\<nome da instância \> .|  
  
## <a name="explanation"></a>Explicação  
 Uma pasta não pode ser criada abaixo de %userprofile%.  
  
## <a name="user-action"></a>Ação do usuário  
  
