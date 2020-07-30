---
title: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: a7c5ce08-8841-49a3-b252-116807ba469a
author: stevestein
ms.author: sstein
ms.openlocfilehash: b07c4eebc34872868da61d7af633d29f1758e313
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246061"
---
# <a name="localdb_error_instance_exists_with_lower_version"></a>LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |
| --------- | ----- |
|Nome do Produto|SQL Server|  
|ID do evento|258|  
|Origem do Evento|Runtime de banco de dados local do SQL Server 12.0|  
|Componente|API do runtime de banco de dados local|  
|Texto da mensagem|Não é possível criar a instância do Banco de Dados Local com a versão especificada. Já existe uma instância com o mesmo nome, mas ela pertence a uma versão inferior à especificada.|  
  
## <a name="explanation"></a>Explicação  
 A instância especificada já existe, mas sua versão é inferior à solicitada.  
  
## <a name="user-action"></a>Ação do usuário  
 Exclua a instância existente e repita a operação.  
  
  
