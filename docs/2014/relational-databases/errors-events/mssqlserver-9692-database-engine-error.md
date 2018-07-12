---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d885e4da6d2da28a7e14fd82062e548f8b36b829
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424935"
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
 Executar `netstat -aon` para determinar qual programa está usando a porta. Desabilite esse aplicativo ou especifique outra porta para o Service Broker.  
  
  
