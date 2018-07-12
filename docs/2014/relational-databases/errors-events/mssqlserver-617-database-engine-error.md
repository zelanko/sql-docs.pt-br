---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f79f2f585eeffde4cb7e81a322a7b5c089f5212a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430991"
---
# <a name="mssqlserver617"></a>MSSQLSERVER_617
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|617|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NODESHASH|  
|Texto da mensagem|O descritor da ID de objeto %ld na ID de banco de dados %d não foi encontrado na tabela de hash durante a tentativa de remoção do hash. Uma entrada está ausente em uma tabela de trabalho. Execute a consulta novamente. Se um cursor estiver envolvido, feche e abra o cursor novamente.|  
  
## <a name="explanation"></a>Explicação  
 O SQL Server não pode localizar a tabela de trabalho da entrada específica.  
  
## <a name="user-action"></a>Ação do usuário  
  
1.  Se um cursor estiver envolvido, feche e reabra o cursor.  
  
2.  Execute a consulta novamente.  
  
  
