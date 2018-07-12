---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2df27a5e730b67ea9c95c9b3f1eca52204659f0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427975"
---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|5245|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|Texto da mensagem|ID de objeto O_ID (objeto 'NAME'): DBCC não pôde obter um bloqueio nesse objeto porque o tempo limite da solicitação de bloqueio foi ultrapassado. Esse objeto foi ignorado e não será processado.|  
  
## <a name="explanation"></a>Explicação  
 O limite de tempo do bloqueio expirou enquanto DBCC estava aguardando um bloqueio de tabela para o objeto especificado.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute o comando DBCC novamente.  
  
  
