---
title: Propriedades do assinante| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb33098d9a66bd9cd71ad0d2ba446499e9789b76
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="subscriber-properties"></a>Propriedades do Assinante
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A caixa de diálogo **Propriedades do Assinante** contém informações relevantes para Assinantes que executam versões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="options"></a>Opções  
 **Conexão do Agente com o Assinante**  
 O contexto no qual o Agente de Distribuição e o Agente de Mesclagem se conectam do Distribuidor ao Assinante. Isso só se aplica a versões anteriores do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Selecione **Representar conta de processo do agente** para efetuar conexões com o Assinante usando o contexto de conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Distribuidor ou especifique **Autenticação do SQL Server**e insira um valor para **Logon** e **Senha**. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você selecione **Representar conta de processo do agente**.  
  
 Para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, as informações de conexão são especificadas para cada assinatura no Assistente para Nova Assinatura e pode ser alterada na caixa de diálogo **Propriedades da Assinatura** .  
  
 **Agendamentos Padrão de Agente**  
 O agendamento padrão usado no Assistente para Nova Assinatura para Assinantes que executam versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 **Diversos**  
 Inclui informações sobre o Assinante e o tipo de Assinante.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Referência de propriedades &#40;Replicação&#41;](../../relational-databases/replication/properties-reference-replication.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
