---
title: "Propriedades de Publica&#231;&#227;o, Geral | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.pubproperties.general.f1"
ms.assetid: 7912362f-c4d6-4f60-bd39-dee1f656ed18
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Propriedades de Publica&#231;&#227;o, Geral
  O **geral** página o **Propriedades de publicação** caixa de diálogo contém informações básicas sobre a publicação, incluindo nome, descrição e a política de expiração da assinatura.  
  
## Opções  
 **Nome**  
 O nome da publicação (somente leitura).  
  
 **Banco de dados**  
 O nome do banco de dados de publicação (somente leitura).  
  
 **Descrição**  
 A descrição da publicação.  
  
 **Tipo**  
 O tipo da publicação (somente leitura).  
  
 **Validade da assinatura**  
 Selecione uma das opções para validade da assinatura: **as assinaturas nunca expiram** ou **as assinaturas expiram**, com um período de tempo explícito (**intervalo**).  
  
 Para publicações de instantâneo e transacionais, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você aceite o padrão de **as assinaturas nunca expiram**.  
  
 Para replicação de mesclagem, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você aceite o padrão de **as assinaturas expiram** e definido como um valor inferior possível para **intervalo**. Como o período de validade da assinatura aumenta, o mesmo ocorre com os metadados armazenados, que podem afetar desempenho. Equilibre a necessidade de desconectar os Assinantes ou simplesmente não sincronize por um período estendido em questões de desempenho potencial de armazenamento e processamento de grande quantidade de metadados.  
  
 Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **nível de compatibilidade**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. apenas para publicações de mesclagem. Selecione versão mínima requerida do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Assinantes que sincronizam com essa publicação. Há várias regras associadas com a determinação do nível de compatibilidade.  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizar e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  