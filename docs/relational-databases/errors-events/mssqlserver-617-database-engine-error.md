---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f5078c98445587dbf8c8b99fa18fed4df2ca5846
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67951662"
---
# <a name="mssqlserver_617"></a>MSSQLSERVER_617
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|617|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NODESHASH|  
|Texto da mensagem|O descritor da ID de objeto %ld na ID de banco de dados %d não foi encontrado na tabela de hash durante a tentativa de remoção do hash. Uma entrada está ausente em uma tabela de trabalho. Execute a consulta novamente. Se um cursor estiver envolvido, feche e abra o cursor novamente.|  
  
## <a name="explanation"></a>Explicação  
O SQL Server não pode localizar a tabela de trabalho da entrada específica.  
  
## <a name="user-action"></a>Ação do usuário  
  
1.  Se um cursor estiver envolvido, feche e reabra o cursor.  
  
2.  Execute a consulta novamente.  
  
