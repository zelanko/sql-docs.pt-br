---
title: MSSQLSERVER_9004 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 54a5b9a70fee2e85c4057f70f22e1b38a5d39354
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761851"
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
  
  
