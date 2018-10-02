---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 91d4f578601710861d4517cc8646f4ff0a6afaf8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741534"
---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
