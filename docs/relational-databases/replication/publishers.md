---
title: "Publicadores | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.configuredistributionwizard.enablepublishers.f1"
ms.assetid: 116cd6a5-32ac-4273-81a2-d184408e0f07
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Publicadores
  Você pode dar permissão para que outros Publicadores usem este Distribuidor. Esteja ciente de que habilitar um Publicador a usar esse servidor como seu Distribuidor remoto não faz daquele servidor um Publicador. Você deve se conectar ao Publicador, configurá-lo para publicação e escolher esse servidor como o Distribuidor. Você pode configurar o Publicador e escolher um Distribuidor pelo Assistente para Nova Publicação.  
  
 Os servidores selecionados como Publicadores usarão o banco de dados de distribuição especificado na página **Banco de Dados de Distribuição** deste assistente. Se você quiser usar um banco de dados de distribuição diferente, não habilite o Publicador neste momento. Em vez disso, use a caixa de diálogo **Propriedades do Distribuidor** para adicionar Publicadores depois que você concluir o Assistente para Configurar a Distribuição.  
  
## Opções  
 **Publicadores**  
 Selecione os servidores que têm permissão para usar esse Distribuidor. Clique no botão Propriedades (**...**) ao lado de um editor para exibir e definir propriedades adicionais.  
  
 **Adicionar**  
 Se o servidor que você deseja permitir não estiver listado, clique em **Add** para adicionar um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Editor ou editor Oracle à lista de editores disponíveis.  
  
## Consulte também  
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)  
  
  