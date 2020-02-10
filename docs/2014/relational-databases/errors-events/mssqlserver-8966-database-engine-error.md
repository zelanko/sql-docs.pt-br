---
title: MSSQLSERVER_8966 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dee5b45aac6518517434595b0f26ce18d219866b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62913158"
---
# <a name="mssqlserver_8966"></a>MSSQLSERVER_8966
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|8966|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|Texto da mensagem|Não foi possível ler e travar a página P_ID com o tipo de trava TYPE. Falha em OPERATION.|  
  
## <a name="explanation"></a>Explicação  
 Houve uma falha na leitura da página ou não foi possível usar uma trava em uma página PFS ou GAM. Pode haver um tempo limite de trava ou outras mensagens acompanhantes no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Ação do usuário  
 Procure essas mensagens no log de erros SQL e corrija os erros.  
  
  
