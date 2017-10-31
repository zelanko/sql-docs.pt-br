---
title: MSSQLSERVER_1807 | Microsoft Docs
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
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e7102630e638d891345c47ed8d9f92700fde39aa
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1807|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|CANNOT_EX_LOCK|  
|Texto da mensagem|Não foi possível obter bloqueio exclusivo no banco de dados '%.*ls'. Tente novamente a operação mais tarde.|  
  
## <a name="explanation"></a>Explicação  
Uma operação que exigia acesso exclusivo ao banco de dados não pôde obtê-lo.  
  
## <a name="user-action"></a>Ação do usuário  
Desconecte todas as conexões com esse banco de dados ou tente a consulta novamente mais tarde.  
  

