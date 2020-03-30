---
title: MSSQL_ENG014144 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014144 error
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c43395fffe934756bb69e0d094a3e6637adcedad
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76286494"
---
# <a name="mssql_eng014144"></a>MSSQL_ENG014144
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|14144|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não é possível descartar o Assinante '%s'. Existem assinaturas para ele no banco de dados de publicação '%s'.|  
  
## <a name="explanation"></a>Explicação  
 Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada como Assinante não pode ser removida da função de Assinante enquanto houver assinaturas ativas configuradas para a instância.  
  
## <a name="user-action"></a>Ação do usuário  
 Descarte todas as assinaturas associadas antes de tentar alterar o status Assinante da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
1.  Execute [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) no banco de dados de publicação no Publicador para encontrar assinaturas.  
  
2.  Execute [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md) no banco de dados de publicação para remover assinaturas.  

## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
