---
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
author: stevestein
ms.author: sstein
ms.openlocfilehash: 86a76c02f6fbd2d4d47772950fa08af656701ac0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68011015"
---
# <a name="localdb_error_too_many_shared_instances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|287|  
|Origem do Evento|Runtime de banco de dados local do SQL Server 12.0|  
|Componente|API do runtime de banco de dados local|  
|Texto da mensagem|Há muitas instâncias compartilhadas e não podemos gerar um Nome da Instância de Usuário exclusivo. Descompartilhe algumas das instâncias compartilhadas existentes.|  
  
## <a name="explanation"></a>Explicação  
 Há muitas instâncias compartilhadas e não podemos gerar um Nome da Instância de Usuário exclusivo.  
  
## <a name="user-action"></a>Ação do usuário  
 Descompartilhe uma ou mais das instâncias compartilhadas do Runtime do Banco de Dados Local e tente novamente.  
  
  
