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
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014144 error
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 49be2d02192109607ace90021bfd8901817091ff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217036"
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
  
  
