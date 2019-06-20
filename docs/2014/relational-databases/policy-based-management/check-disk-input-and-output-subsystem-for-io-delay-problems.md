---
title: Verificar subsistema de entrada e saída de disco quanto a problemas de atraso de E/S | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5cdcc410cc83d7f7fa53d937f6011ad2624655fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157341"
---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>Verificar o subsistema de entrada e saída de disco para problemas de atraso de E/S
  Esta regra verifica o log de eventos quanto à mensagem de erro 833. Esta mensagem indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emitiu uma solicitação de leitura ou gravação de disco, e que a solicitação demorou mais de 15 segundos para retornar. Esse erro é informado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e indica um problema com o subsistema de E/S do disco. Atrasos longos podem danificar seriamente o desempenho do ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Solucione este erro procurando mensagens de erros relacionados a hardware no log de eventos de sistema. Examine também os logs específicos do hardware, se estiverem disponíveis.  
  
 Use o Monitor de Desempenho para examinar os seguintes contadores:  
  
-   Transferência média do disco por segundo  
  
-   Comprimento médio da fila de disco  
  
-   Comprimento da fila atual de disco  
  
 Por exemplo, o tempo médio de Disco seg/Transferência em um computador executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente é inferior a 15 milissegundos. Se o valor médio de Disco seg/Transferência aumentar, isso indica que o subsistema de E/S do disco não está acompanhando da melhor maneira possível o ritmo da demanda de E/S.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [MSSQLSERVER_833](../errors-events/mssqlserver-833-database-engine-error.md)  
  
 [Artigo 897284 da Base de Dados de Conhecimento Microsoft](https://go.microsoft.com/fwlink/?linkid=117743)  
  
 [Fundamentos de E/S do SQL Server, Capítulo 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))  
  
  
