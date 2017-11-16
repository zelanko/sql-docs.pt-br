---
title: MSSQLSERVER_17132 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 2701e2c6207c146d9aeb75568659f5f8e6f3d4d4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver17132"></a>MSSQLSERVER_17132
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17132|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|INIT_NODESSPACE|  
|Texto da mensagem|Ocorreu uma falha na inicialização do servidor devido à falta de memória para o descritor. Reduza a carga de memória dispensável ou aumente a memória do sistema.|  
  
## <a name="explanation"></a>Explicação  
Falha ao alocar memória suficiente para armazenar o descritor interno do servidor.  
  
## <a name="user-action"></a>Ação do usuário  
Adicione mais memória ao computador. As etapas genéricas para a solução de problemas de memória podem ser úteis.  
  
