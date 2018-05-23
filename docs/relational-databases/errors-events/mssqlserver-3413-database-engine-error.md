---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 93da8503cf190a0c770e25891416f784b15d85db
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3413|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|MARKDB|  
|Texto da mensagem|ID do banco de dados %d. Não foi possível marcar o banco de dados como suspeito. Falha no exame de Getnext NC em sys.databases.database_id. Consulte os erros anteriores no log de erros para identificar a causa e corrigir os problemas associados.|  
  
## <a name="explanation"></a>Explicação  
Houve uma falha inesperada ao tentar marcar um banco de dados de usuário como SUSPECT no catálogo. O estado SUSPECT não será persistente.  
  
## <a name="user-action"></a>Ação do usuário  
Consulte os erros anteriores e corrija o problema.  
  
