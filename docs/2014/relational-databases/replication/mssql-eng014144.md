---
title: MSSQL_ENG014144 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014144 error
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7e4d3991806fe3f2275fd94f3ffbacc1c94ccbd8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116895"
---
# <a name="mssqleng014144"></a>MSSQL_ENG014144
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14144|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não é possível descartar o Assinante '%s'. Existem assinaturas para ele no banco de dados de publicação '%s'.|  
  
## <a name="explanation"></a>Explicação  
 Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada como Assinante não pode ser removida da função de Assinante enquanto houver assinaturas ativas configuradas para a instância.  
  
## <a name="user-action"></a>Ação do usuário  
 Descarte todas as assinaturas associadas antes de tentar alterar o status Assinante da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
1.  Execute [sp_helpsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) no banco de dados de publicação no Publicador para encontrar assinaturas.  
  
2.  Execute [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql) no banco de dados de publicação para remover assinaturas.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)   
 [Assinar publicações](subscribe-to-publications.md)  
  
  
