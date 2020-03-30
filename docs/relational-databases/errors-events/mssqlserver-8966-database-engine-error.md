---
title: MSSQLSERVER_8966 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8dff6385227c8ec498187541f4c8f8653ace15b5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68074289"
---
# <a name="mssqlserver_8966"></a>MSSQLSERVER_8966
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
