---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6b6ba95771aafffa5a322ffa1b7443419936addd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053440"
---
# <a name="mssqlserver_9692"></a>MSSQLSERVER_9692
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|9692|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SB2_CANT_LISTEN_PORT_IN_USE|  
|Texto da mensagem|O protocolo de transporte %S_MSG não pode escutar na porta %d porque ela está em uso por outro processo.|  
  
## <a name="explanation"></a>Explicação  
 Outro programa no computador está usando a porta TCP indicada.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute `netstat -aon` para determinar qual programa está usando a porta. Desabilite esse aplicativo ou especifique outra porta para o Service Broker.  
  
  
