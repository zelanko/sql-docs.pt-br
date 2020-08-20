---
description: MSSQLSERVER_17884
title: MSSQLSERVER_17884 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2f7ec5ee211f87d61b39d64c5423b2c7c6612a28
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456328"
---
# <a name="mssqlserver_17884"></a>MSSQLSERVER_17884
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|17884|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SRV_SCHEDULER_DEADLOCK|  
|Texto da mensagem|Novas consultas atribuídas ao processo no Nó %d não foram selecionadas por um thread de trabalho nos últimos %d segundos. Consultas de execução longa ou bloqueios podem contribuir para essa condição e afetar o tempo de resposta do cliente. Use a opção de configuração "max worker threads" (máximo de threads de trabalho) para aumentar o número de threads permitidos ou otimizar as consultas que estão sendo executadas atualmente.  SQL Process Utilization: %d%%. Sistema inativo: %d%%.|  
  
## <a name="explanation"></a>Explicação  
Não há sinal de progresso nos agendadores e isso pode ser causado por deadlocks onde nenhum dos threads pode avançar e/ou nenhum trabalho novo pode ser selecionado e processado. Caso a utilização do processo esteja baixa, outros processos na máquina podem estar causando a privação de processo da CPU.  
  
## <a name="user-action"></a>Ação do usuário  
Determine porque existe um bloqueio e porque nenhum progresso está sendo feito. Em seguida, resolva a situação de maneira adequada. Caso a utilização do processo esteja baixa, verifique a carga no sistema causada por outros processos.  
  
