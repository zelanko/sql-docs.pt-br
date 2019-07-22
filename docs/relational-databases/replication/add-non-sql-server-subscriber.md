---
title: Adicionar assinante não SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6b188b7ec3b108a32a52ce888d4dfb1b5a064804
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929782"
---
# <a name="add-non-sql-server-subscriber"></a>Adicionar Assinante não SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A replicação oferece suporte à criação de assinaturas push para publicações de instantâneo e transacionais para Assinantes Oracle e IBM DB2.  
  
## <a name="options"></a>Opções  
 **Tipo de Assinante a adicionar**  
 Selecione um Assinante Oracle ou um Assinante IBM DB2. Para obter mais informações sobre o suporte para esses Assinantes, consulte [Assinantes não SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 **Nome da fonte de dados**  
 O nome usado para localizar o banco de dados em uma rede. A replicação produz uma sequência de conexão para o banco de dados usando o nome da fonte de dados, combinando com o logon, senha e qualquer opção de conexão especificada na página **Segurança do Agente de Distribuição** neste assistente.  
  
> [!NOTE]
>  The data source name and connection string are not validated by [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] until the Distribution Agent attempts to initialize the subscription.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma assinatura para um assinante não SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
