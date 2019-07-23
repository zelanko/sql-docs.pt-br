---
title: MSSQLSERVER_17132 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 335ba6a544023fd4eec16cd7461e2e17c224020f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68131798"
---
# <a name="mssqlserver17132"></a>MSSQLSERVER_17132
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
