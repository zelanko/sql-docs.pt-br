---
title: "Propriedades de Publica&#231;&#227;o, Lista de Acesso &#224; Publica&#231;&#227;o | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.pubproperties.publicationaccesslist.f1"
ms.assetid: 9587bb9e-c66c-4e70-8171-09b943ec2d50
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Propriedades de Publica&#231;&#227;o, Lista de Acesso &#224; Publica&#231;&#227;o
  O **lista de acesso da publicação** página de **Propriedades de publicação** caixa de diálogo permite adicionar e remover logons, contas e grupos da lista de acesso de publicação (PAL). A PAL é o mecanismo primário de segurança do Publicador. Quando você cria uma publicação, a replicação cria uma PAL para a publicação. A PAL, cuja função é semelhante à lista de controle de acesso do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, contém uma lista de logons, contas e grupos com acesso garantido à publicação.  
  
 Quando um Assinante se conecta ao Publicador ou ao Distribuidor e solicita acesso à publicação, o logon do Assinante é comparado com as informações de autenticação na PAL. Isso fornece segurança adicional ao Publicador, impedindo que o logon do Publicador e do Distribuidor seja usado por uma ferramenta cliente para executar modificações no Publicador diretamente. Para obter mais informações, consulte [proteger o publicador](../../relational-databases/replication/security/secure-the-publisher.md).  
  
## Opções  
 **Adicionar**  
 Adicione uma nova entrada à lista. Você só pode adicionar os nomes de logon, conta ou grupo já definidos no Publicador e no Distribuidor Eles serão definidos em ambos os servidores se as contas de domínio ou contas locais tiverem sido criadas em ambos.  
  
 **Remover**  
 Remova a entrada selecionada da lista.  
  
 **Remover Tudo**  
 Remova todas as entradas da lista.  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizar e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  