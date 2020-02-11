---
title: MSSQLSERVER_17132 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 871c5961b1c878e8eaad9d536731c57e71bb40ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915315"
---
# <a name="mssqlserver_17132"></a>MSSQLSERVER_17132
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|17132|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|INIT_NODESSPACE|  
|Texto da mensagem|Ocorreu uma falha na inicialização do servidor devido à falta de memória para o descritor. Reduza a carga de memória dispensável ou aumente a memória do sistema.|  
  
## <a name="explanation"></a>Explicação  
 Falha ao alocar memória suficiente para armazenar o descritor interno do servidor.  
  
## <a name="user-action"></a>Ação do usuário  
 Adicione mais memória ao computador. As etapas genéricas para a solução de problemas de memória podem ser úteis.  
  
  
