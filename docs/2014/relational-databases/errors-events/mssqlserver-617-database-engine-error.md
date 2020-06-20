---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dedf0b9ae26e7c2c1bb2c3251a1df10a3577f96d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053777"
---
# <a name="mssqlserver_617"></a>MSSQLSERVER_617
    
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
  
  
