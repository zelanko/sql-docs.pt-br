---
title: Verificar o subsistema de E/S do disco para problemas de atraso de E/S
description: Saiba como habilitar uma política para verificar o subsistema de E/S de disco em busca de problemas de atraso de E/S verificando o log de eventos para ver se a mensagem de erro 833 é exibida para o gerenciamento baseado em políticas com o SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f8c880438491f697d57134b5004129eef38a7fe8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749516"
---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>Verificar o subsistema de entrada e saída de disco para problemas de atraso de E/S
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regra verifica o log de eventos quanto à mensagem de erro 833. Esta mensagem indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emitiu uma solicitação de leitura ou gravação de disco, e que a solicitação demorou mais de 15 segundos para retornar. Esse erro é informado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e indica um problema com o subsistema de E/S do disco. Atrasos longos podem danificar seriamente o desempenho do ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Solucione este erro procurando mensagens de erros relacionados a hardware no log de eventos de sistema. Examine também os logs específicos do hardware, se estiverem disponíveis.  
  
 Use o Monitor de Desempenho para examinar os seguintes contadores:  
  
-   Transferência média do disco por segundo  
  
-   Comprimento médio da fila de disco  
  
-   Comprimento da fila atual de disco  
  
 Por exemplo, o tempo médio de Disco seg/Transferência em um computador executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente é inferior a 15 milissegundos. Se o valor médio de Disco seg/Transferência aumentar, isso indica que o subsistema de E/S do disco não está acompanhando da melhor maneira possível o ritmo da demanda de E/S.  
  
## <a name="for-more-information"></a>Para obter mais informações  
   
  
 [Artigo 897284 da Base de Dados de Conhecimento Microsoft](https://go.microsoft.com/fwlink/?linkid=117743)  
  
 [Fundamentos de E/S do SQL Server, Capítulo 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))
