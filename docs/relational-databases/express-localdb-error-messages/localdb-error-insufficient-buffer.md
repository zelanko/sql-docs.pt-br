---
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
author: stevestein
ms.author: sstein
ms.openlocfilehash: cdb7c78a8301ec11ddd54329c4c68943ea66afd2
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245186"
---
# <a name="localdb_error_insufficient_buffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |
| --------- | ----- |
|Nome do Produto|SQL Server|  
|ID do evento|276|  
|Origem do Evento|Runtime de banco de dados local do SQL Server 12.0|  
|Componente|API do runtime de banco de dados local|  
|Texto da mensagem|O buffer passado ao método de API da instância do Banco de Dados Local tem tamanho insuficiente.|  
  
## <a name="explanation"></a>Explicação  
 O buffer de entrada é muito curto e o truncamento não foi solicitado.  
  
## <a name="user-action"></a>Ação do usuário  
 Forneça um buffer do tamanho especificado.  
  
  
