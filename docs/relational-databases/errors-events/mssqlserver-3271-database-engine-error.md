---
title: MSSQLSERVER_3271 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3271 (Database Engine error)
ms.assetid: 21b8de4b-6624-4163-9561-1a6cc8fe3d51
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2acc1e53cfd5bb0fd00668f3c5ba99559d2cd6e8
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3271"></a>MSSQLSERVER_3271
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3271|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DMPIO_IO_ERROR|  
|Texto da mensagem|Um erro de E/S não recuperável aconteceu no arquivo "%ls": %ls.|  
  
## <a name="explanation"></a>Explicação  
Trata-se de um erro geral que ocorre quando o sistema operacional gera um erro ao executar E/S durante uma operação de backup ou restauração. Na maioria das situações, isso ocorre simplesmente porque a mídia de backup está cheia.  
  
O erro pode incluir um texto adicional do sistema operacional indicando que o disco está cheio. Ao executar uma operação de backup ou restauração com software de terceiros, pode aparecer uma mensagem adicional indicando que o backup falhou. A mensagem pode ter a seguinte aparência:  
  
```  
"2005-08-02 16:05:16.04 spid55 Error: 18210, Severity: 16, State: 1.  
 2005-08-02 16:05:16.04 spid55 BackupVirtualDeviceFile  
::RequestDurableMedia: Flush failure on backup device 'VDINULL'.   
Operating system error 995(The I/O operation has been aborted because   
of either a thread exit or an application request.)."  
```  
  
Isso indica que o software de backup solicitou a finalização do processo de backup ou restauração.  
  
## <a name="user-action"></a>Ação do usuário  
Execute as seguintes tarefas, conforme apropriado:  
  
-   Analise as mensagens de erro do sistema e as mensagens de erro do SQL Server que ocorreram antes desse processo para identificar a causa da falha.  
  
-   Verifique se a mídia de backup e restauração tem espaço suficiente.  
  
-   Corrija qualquer erro gerado pelo software de backup e restauração de terceiros.  
  

