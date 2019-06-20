---
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9be09d2579e074c1dfc5d34d721f2918f2022112
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63044011"
---
# <a name="localdberrortoomanysharedinstances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
    
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
  
  
