---
title: MSSQL_ENG014005 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014005 error
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 2331221ea8a15935b91a7ba8cc6691dd27cec4e3
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770497"
---
# <a name="mssqleng014005"></a>MSSQL_ENG014005
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14005|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não foi possível descartar a publicação. Existe uma assinatura para ela.|  
  
## <a name="explanation"></a>Explicação  
 Você tentou descartar uma publicação que tem uma ou mais assinatura associadas. Uma publicação pode ser descartada somente se não houver nenhuma assinatura associada.  
  
## <a name="user-action"></a>Ação do usuário  
 Descarte as assinaturas antes de descartar a publicação. Se você usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para descartar a publicação, haverá a opção de descartar automaticamente todas as assinaturas associadas antes de descartar a publicação. Se você usar procedimentos armazenados, primeiro será necessário descartar explicitamente as assinaturas. Para obter mais informações, consulte [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) e [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 Se não existirem assinaturas para a publicação ou se o erro for exibido ao criar uma publicação, talvez exista uma assinatura anterior que não foi limpa completamente quando você tentou removê-la. Execute [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) no banco de dados para remover todas as configurações e todos os objetos relacionados à replicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
