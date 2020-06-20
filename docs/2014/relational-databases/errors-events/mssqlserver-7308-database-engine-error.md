---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9978f35ebe41eeda1470220772f87e83ab1ad942
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053769"
---
# <a name="mssqlserver_7308"></a>MSSQLSERVER_7308
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|7308|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|RMT_STA_DISABLED|  
|Texto da mensagem|Não é possível usar o provedor OLE DB '%ls' para consultas distribuídas porque ele está configurado para execução no modo STA.|  
  
## <a name="explanation"></a>Explicação  
 Você usou um provedor OLE DB configurado para execução no modo STA. Provedores do OLE DB executados no modo STA não podem ser usados para consultas distribuídas.  
  
## <a name="user-action"></a>Ação do usuário  
 Para resolver o erro, configure o provedor para execução no modo MTA. Se o provedor não tiver suporte para MTA e não for possível atualizá-lo para uma versão com suporte a MTA, considere configurá-lo para execução fora do processo. O fornecedor do provedor deverá ser capaz de informar se o provedor dá suporte para MTA ou execução fora do processo.  
  
  
