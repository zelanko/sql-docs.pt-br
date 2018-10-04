---
title: Propriedades do distribuidor, Geral | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distproperties.general.f1
helpviewer_keywords:
- Distributor Properties dialog box
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 04d0ae695a5851c56944e709dfa562963e54b7e8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087286"
---
# <a name="distributor-properties-general"></a>Propriedades do Distribuidor, Geral
  A página **Geral** da caixa de diálogo **Propriedades do Distribuidor** permite adicionar e excluir bancos de dados de distribuição e definir propriedades do banco de dados de distribuição.  
  
 O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional. Em muitos casos, um único banco de dados de distribuição é suficiente. Porém, se vários Publicadores usarem um único Distribuidor, considere criar um banco de dados de distribuição para cada Publicador. Fazer isso assegura que os dados que fluem por cada banco de dados de distribuição são distintos.  
  
## <a name="options"></a>Opções  
 **Bancos de dados**  
 A grade de propriedades dos **Bancos de Dados** mostra as nome e as propriedades de retenção dos bancos de dados de distribuição no Distribuidor. **Retenção de Transação** é o período de tempo em que as transações são armazenadas para replicação transacional (a retenção da transação também é conhecida como retenção de distribuição). **Retenção de Histórico** é o período de tempo em que os metadados de histórico são armazenados para todos os tipos de replicação. Para mais informações sobre retenção de distribuição, consulte [Desativação e expiração da assinatura](subscription-expiration-and-deactivation.md).  
  
 Clique no botão de propriedades (**...**) na grade de propriedades de **Bancos de dados** para iniciar a caixa de diálogo **Propriedades do Banco de Dados de Distribuição** .  
  
 **Nova**  
 Clique para criar um novo banco de dados de distribuição.  
  
 **Delete (excluir)**  
 Selecione um banco de dados de distribuição existente na grade de propriedade de **Bancos de Dados** e clique em **Excluir** para excluir o banco de dados. O banco de dados de distribuição não poderá ser excluído se houver apenas esse banco de dados; cada distribuidor deve ter pelo menos um banco de dados de distribuição. Para excluir todos os bancos de dados de distribuição, você deve desabilitar a distribuição no computador. Para obter mais informações, consulte [Desabilitar a publicação e a distribuição](disable-publishing-and-distribution.md).  
  
 **Padrões de Perfil**  
 Clique para acessar perfis de agente de replicação na caixa de diálogo **Perfis de Agente** . Para obter mais informações sobre perfis, consulte [Replication Agent Profiles](agents/replication-agent-profiles.md).  
  
## <a name="see-also"></a>Consulte também  
 [Configurar Distribuição](configure-distribution.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](view-and-modify-distributor-and-publisher-properties.md)  
  
  
