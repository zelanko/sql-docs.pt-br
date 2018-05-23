---
title: MSSQLSERVER_9004 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e3adf2903a0b8b0861f9a773531d5fea1b6bff5a
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver9004"></a>MSSQLSERVER_9004
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9004|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LOG_CORRUPT|  
|Texto da mensagem|Erro ao processar o log do banco de dados '%.*ls'.  Se possível, restaure do backup. Se não houver um backup disponível, talvez seja necessário recriar o log.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu um erro ao processar o log durante a reversão, a recuperação ou a replicação. Isso pode indicar um erro detectado pelo sistema operacional ou um erro de consistência interno detectado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Ação do usuário  
Uma das ações seguintes poderá corrigir esse erro:  
  
-   Faça uma restauração a partir do backup.  
  
-   Refaça o log.  
  
Verifique também o evento de sistema e logs de erros para identificar problemas no sistema que podem ter causado o erro.  
  
