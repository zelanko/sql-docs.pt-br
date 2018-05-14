---
title: Publicadores | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sql13.rep.configuredistributionwizard.enablepublishers.f1
ms.assetid: 116cd6a5-32ac-4273-81a2-d184408e0f07
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6000afdf73e2014353bd6cb1f63e84b730f3aa7f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="publishers"></a>Publicadores
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode dar permissão para que outros Publicadores usem este Distribuidor. Esteja ciente de que habilitar um Publicador a usar esse servidor como seu Distribuidor remoto não faz daquele servidor um Publicador. Você deve se conectar ao Publicador, configurá-lo para publicação e escolher esse servidor como o Distribuidor. Você pode configurar o Publicador e escolher um Distribuidor pelo Assistente para Nova Publicação.  
  
 Os servidores selecionados como Publicadores usarão o banco de dados de distribuição especificado na página **Banco de Dados de Distribuição** deste assistente. Se você quiser usar um banco de dados de distribuição diferente, não habilite o Publicador neste momento. Em vez disso, use a caixa de diálogo **Propriedades do Distribuidor** para adicionar Publicadores depois que você concluir o Assistente para Configurar a Distribuição.  
  
## <a name="options"></a>Opções  
 **Publicadores**  
 Selecione os servidores que têm permissão para usar esse Distribuidor. Clique no botão de propriedades (**...**) próximo ao Publicador para exibir e definir propriedades adicionais.  
  
 **Adicionar**  
 Se o servidor que você deseja permitir não estiver na lista, clique em **Adicionar** para adicionar um Editor [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um Editor Oracle à lista de Publicadores disponíveis.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Criar uma publicação](../../relational-databases/replication/publish/create-a-publication.md)  
  
  
