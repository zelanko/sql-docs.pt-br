---
description: Propriedades do Assinante
title: Propriedades do assinante| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 366740d950e249d6ad18e97af3094208d4d849fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493869"
---
# <a name="subscriber-properties"></a>Propriedades do Assinante
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  A caixa de diálogo **Propriedades do Assinante** contém informações relevantes para os Assinantes que executam versões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]

  
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
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
