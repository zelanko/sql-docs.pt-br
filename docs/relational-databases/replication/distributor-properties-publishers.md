---
title: "Propriedades do Distribuidor, Publicadores | Microsoft Docs"
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
  - "sql13.rep.configdistwizard.distproperties.publishers.f1"
helpviewer_keywords: 
  - "caixa de diálogo Propriedades do Distribuidor"
ms.assetid: 31c81898-11ca-4d2f-afea-2fbc71e19ce4
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Propriedades do Distribuidor, Publicadores
  A página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor** permite habilitar Publicadores a usarem esse Distribuidor. Você também pode definir propriedades associadas a esses Publicadores. Esteja ciente de que habilitar um Publicador a usar esse servidor como seu Distribuidor remoto não faz daquele servidor um Publicador. Você deve se conectar ao Publicador, configurá-lo para publicação e escolher esse servidor como o Distribuidor. Você pode configurar o Publicador e escolher um Distribuidor pelo Assistente para Nova Publicação.  
  
## Opções  
 **Publicadores**  
 Selecione os servidores que têm permissão para usar esse Distribuidor. Clique no botão propriedades **(…)** ao lado de um editor para exibir e definir propriedades adicionais.  
  
 **Adicionar**  
 Se o servidor que você deseja permitir não estiver listado, clique em **Add** para adicionar um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Editor ou editor Oracle à lista de editores disponíveis. Se o servidor que você adicionar for o primeiro a usar esse Distribuidor como remoto, você será solicitado a fornecer uma senha de vínculo administrativo.  
  
 **Senha de vínculo administrativo**  
 Use para especificar ou atualizar a senha para a conexão que a replicação faz entre o Editor e o distribuidor remoto usando o **distributor_admin** logon:  
  
-   Se o  Distribuidor servir somente como Distribuidor local, essa senha será gerada aleatoriamente e configurada automaticamente.  
  
-   Se o Distribuidor já tiver um Publicador remoto, uma senha terá sido fornecida inicialmente nessa página ou na página **Senha do Distribuidor** do Assistente para Configurar Distribuição.  
  
-   Se você ativar o primeiro Publicador remoto para esse Distribuidor, você será solicitado a inserir uma senha.  
  
 Para obter mais informações sobre segurança para distribuidores, consulte [proteger o distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## Consulte também  
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  