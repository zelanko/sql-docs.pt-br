---
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd7250089e442cd14283b3500aece8a8b2125d7e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="localdberrortoomanysharedinstances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|287|  
|Origem do evento|Tempo de execução de banco de dados local do SQL Server 12.0|  
|Componente|API do tempo de execução de banco de dados local|  
|Texto da mensagem|Há muitas instâncias compartilhadas e não podemos gerar um Nome da Instância de Usuário exclusivo. Descompartilhe algumas das instâncias compartilhadas existentes.|  
  
## <a name="explanation"></a>Explicação  
 Há muitas instâncias compartilhadas e não podemos gerar um Nome da Instância de Usuário exclusivo.  
  
## <a name="user-action"></a>Ação do usuário  
 Descompartilhe uma ou mais das instâncias compartilhadas do Tempo de Execução do Banco de Dados Local e tente novamente.  
  
  
