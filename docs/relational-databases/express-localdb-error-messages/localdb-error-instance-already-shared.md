---
title: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 35b4d6fa-ebb9-49d3-aaab-d4e37b6f3760
author: stevestein
ms.author: sstein
ms.openlocfilehash: fbbad615b2b4f18e9e46ad931a00e7a2d8bee804
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756911"
---
# <a name="localdb_error_instance_already_shared"></a>LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|284|  
|Origem do Evento|Runtime de banco de dados local do SQL Server 12.0|  
|Componente|API do runtime de banco de dados local|  
|Texto da mensagem|A instância especificada do Banco de Dados Local já está compartilhada.|  
  
## <a name="explanation"></a>Explicação  
 A instância especificada do Banco de Dados Local já está compartilhada com um nome compartilhado diferente.  
  
## <a name="user-action"></a>Ação do usuário  
 Descompartilhe a instância compartilhada antes de compartilhá-la novamente com um nome compartilhado diferente.  
  
  
