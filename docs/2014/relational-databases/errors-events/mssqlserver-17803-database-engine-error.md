---
title: MSSQLSERVER_17803 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 683806941947a6da888264e4d0e4e3807200ef13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62869541"
---
# <a name="mssqlserver_17803"></a>MSSQLSERVER_17803
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|17803|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SRV_NOMEMORY|  
|Texto da mensagem|Ocorreu uma falha de alocação de memória ao estabelecer conexão. Reduce nonessential memory load, or increase system memory. A conexão foi fechada.%.*ls|  
  
## <a name="explanation"></a>Explicação  
 O servidor está sendo executado sem memória.  
  
## <a name="user-action"></a>Ação do usuário  
 Determine o motivo pelo qual o servidor está sendo executado sem memória. Etapas genéricas para a solução de problemas de memória podem ser úteis  
  
  
