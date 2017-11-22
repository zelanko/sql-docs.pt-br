---
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 624c23bd1a916d28a942332bb7dfc737048b28bc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver17053"></a>MSSQLSERVER_17053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17053|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|OS_ERROR|  
|Texto da mensagem|%ls: %ls erros do sistema operacional foram encontrados.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu um erro genérico do sistema operacional.  Não desmarque a informação resultante.  
  
## <a name="user-action"></a>Ação do usuário  
Normalmente, isso ocorre com algum outro erro e pode ser usado para ajudar a diagnosticar essa falha. Os exemplos podem incluir falhas em leituras ou gravações de dados ou em arquivos de log, operações de leitura/gravação no Registro ou outras falhas inesperadas da Win32API.  
  
