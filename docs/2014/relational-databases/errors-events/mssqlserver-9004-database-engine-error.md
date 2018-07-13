---
title: MSSQLSERVER_9004 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c80678bc5463f3cf17d8442afb36c30dcc69534c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429405"
---
# <a name="mssqlserver9004"></a>MSSQLSERVER_9004
    
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
  
  
