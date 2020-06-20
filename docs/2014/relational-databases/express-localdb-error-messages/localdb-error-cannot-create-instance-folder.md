---
title: LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 626b73d3-a257-4b45-82fb-c6299faa0001
author: stevestein
ms.author: sstein
ms.openlocfilehash: b127bedb0dc13c0b8b5a238a8ef104ca9a00bd85
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85051238"
---
# <a name="localdb_error_cannot_create_instance_folder"></a>LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|256|  
|Origem do Evento|Runtime de banco de dados local do SQL Server 12.0|  
|Componente|API do runtime de banco de dados local|  
|Texto da mensagem|Não é possível criar a pasta para a instância do banco de dados local em:%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server local DB\Instances \\<nome da instância \> .|  
  
## <a name="explanation"></a>Explicação  
 Uma pasta não pode ser criada abaixo de %userprofile%.  
  
## <a name="user-action"></a>Ação do usuário  
  
