---
title: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: a7c5ce08-8841-49a3-b252-116807ba469a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b3bc344e3e23ce965a2057628e4662ebe41508d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62990922"
---
# <a name="localdb_error_instance_exists_with_lower_version"></a>LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|258|  
|Origem do Evento|Runtime de banco de dados local do SQL Server 12.0|  
|Componente|API do runtime de banco de dados local|  
|Texto da mensagem|Não é possível criar a instância do Banco de Dados Local com a versão especificada. Já existe uma instância com o mesmo nome, mas ela pertence a uma versão inferior à especificada.|  
  
## <a name="explanation"></a>Explicação  
 A instância especificada já existe, mas sua versão é inferior à solicitada.  
  
## <a name="user-action"></a>Ação do usuário  
 Exclua a instância existente e repita a operação.  
  
  
