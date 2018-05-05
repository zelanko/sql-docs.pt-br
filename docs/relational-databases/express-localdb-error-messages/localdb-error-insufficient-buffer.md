---
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7237a511cd4fa85a02e3ee77a212e52c7a3b9f5b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="localdberrorinsufficientbuffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|276|  
|Origem do evento|Tempo de execução de banco de dados local do SQL Server 12.0|  
|Componente|API do tempo de execução de banco de dados local|  
|Texto da mensagem|O buffer passado ao método de API da instância do Banco de Dados Local tem tamanho insuficiente.|  
  
## <a name="explanation"></a>Explicação  
 O buffer de entrada é muito curto e o truncamento não foi solicitado.  
  
## <a name="user-action"></a>Ação do usuário  
 Forneça um buffer do tamanho especificado.  
  
  
