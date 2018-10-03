---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2af9a604c511c50b542fbacd547afb3e09d7ea54
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201866"
---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
    
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
  
  
