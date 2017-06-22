---
title: MSSQLSERVER_9790 | Microsoft Docs
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
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f7a07e157da848a3201d0a50d6e270988ddf9943
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9790|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|Texto da mensagem|Não é possível rotear a mensagem de entrada. O banco de dados de sistema MSDB que contém informações de roteamento está no modo SINGLE USER.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu um erro ao tentar classificar uma mensagem recebida sem-cabo porque o banco de dados MSDB estava no modo usuário único.  
  
## <a name="user-action"></a>Ação do usuário  
Altere o MSDB para o modo MULTI USER com o comando ALTER DATABASE.  
  

