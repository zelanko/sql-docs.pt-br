---
title: Propriedades do distribuidor, Geral | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.distproperties.general.f1
helpviewer_keywords:
- Distributor Properties dialog box
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e06ffa4473bf9f92509252b851e3e93a6b16beae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="distributor-properties-general"></a>Propriedades do Distribuidor, Geral
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A página **Geral** da caixa de diálogo **Propriedades do Distribuidor** permite adicionar e excluir bancos de dados de distribuição e definir propriedades do banco de dados de distribuição.  
  
 O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional. Em muitos casos, um único banco de dados de distribuição é suficiente. Porém, se vários Publicadores usarem um único Distribuidor, considere criar um banco de dados de distribuição para cada Publicador. Fazer isso assegura que os dados que fluem por cada banco de dados de distribuição são distintos.  
  
## <a name="options"></a>Opções  
 **Bancos de dados**  
 A grade de propriedades dos **Bancos de Dados** mostra as nome e as propriedades de retenção dos bancos de dados de distribuição no Distribuidor. **Retenção de Transação** é o período de tempo em que as transações são armazenadas para replicação transacional (a retenção da transação também é conhecida como retenção de distribuição). **Retenção de Histórico** é o período de tempo em que os metadados de histórico são armazenados para todos os tipos de replicação. Para mais informações sobre retenção de distribuição, consulte [Desativação e expiração da assinatura](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 Clique no botão de propriedades (**...**) na grade de propriedades de **Bancos de dados** para iniciar a caixa de diálogo **Propriedades do Banco de Dados de Distribuição** .  
  
 **Nova**  
 Clique para criar um novo banco de dados de distribuição.  
  
 **Delete (excluir)**  
 Selecione um banco de dados de distribuição existente na grade de propriedade de **Bancos de Dados** e clique em **Excluir** para excluir o banco de dados. O banco de dados de distribuição não poderá ser excluído se houver apenas esse banco de dados; cada distribuidor deve ter pelo menos um banco de dados de distribuição. Para excluir todos os bancos de dados de distribuição, você deve desabilitar a distribuição no computador. Para obter mais informações, consulte [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md).  
  
 **Padrões de Perfil**  
 Clique para acessar perfis de agente de replicação na caixa de diálogo **Perfis de Agente** . Para obter mais informações sobre perfis, consulte [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
