---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 2c7e9da124ed3ec2fb1a0725f2f2c3050cd3484f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9692|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SB2_CANT_LISTEN_PORT_IN_USE|  
|Texto da mensagem|O protocolo de transporte %S_MSG não pode escutar na porta %d porque ela está em uso por outro processo.|  
  
## <a name="explanation"></a>Explicação  
Outro programa no computador está usando a porta TCP indicada.  
  
## <a name="user-action"></a>Ação do usuário  
Execute **netstat -aon** para determinar qual programa está usando a porta. Desabilite esse aplicativo ou especifique outra porta para o Service Broker.  
  
