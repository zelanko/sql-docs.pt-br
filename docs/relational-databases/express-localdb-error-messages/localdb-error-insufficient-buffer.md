---
description: LOCALDB_ERROR_INSUFFICIENT_BUFFER
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 5c0315eb0d4318fd7e6c82ad19676af37e0391d8
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506190"
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
  
  
