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
ms.openlocfilehash: 8be63b3d05bff2ebf90122f66af4297d77376fce
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967816"
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
  
  
