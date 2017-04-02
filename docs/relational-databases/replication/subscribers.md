---
title: "Assinantes | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.subscribers.f1"
helpviewer_keywords: 
  - "Assinantes [replicação do SQL Server]"
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Assinantes
  Especifique o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou não-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes que receberão uma assinatura para a publicação selecionada.  
  
## Opções  
 **Assinantes**  
 Selecione a caixa de seleção na grade para habilitar correspondente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou não-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um assinante da publicação escolhida na fonte de dados de **publicação** página. Se o Assinante não estiver na lista, clique em **Adicionar Assinante** ou **Adicionar Assinante SQL Server**.  
  
 **Banco de dados de assinatura**  
 As informações exibidas no e ações disponíveis desta coluna dependem do tipo de assinante listado no **assinantes** coluna:  
  
-   Para Assinantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selecione um banco de dados de assinatura da lista **Banco de Dados de Assinatura** para criar um novo banco de dados selecionando o comando **Novo banco de dados** na mesma lista.  
  
    > [!NOTE]  
    >  Se você estiver habilitando o Publicador como um Assinante, o banco de dados de assinatura deverá ser diferente do banco de dados de publicação.  
  
-   Para Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o banco de dados de assinatura não é exibido. Especifique o banco de dados, juntamente com outras informações de conexão no **nome da fonte de dados** campo o **Adicionar não SQL Server** caixa de diálogo. Essa caixa de diálogo está disponível clicando **Adicionar assinante** e, em seguida, clicando em **Adicionar assinante não-SQL Server**.  
  
 **Adicionar Assinante**  
 Adicione um servidor à lista de servidores que podem ser habilitados como Assinantes. Esse botão é exibido quando todas as condições seguintes são verdadeiras:  
  
-   A publicação selecionada é uma publicação de instantâneo ou transacional que não oferece suporte a assinaturas de atualização.  
  
    > [!NOTE]  
    >  Se a publicação que você estiver assinando tiver assinaturas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a publicação ainda não tiver sido habilitada como Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], não será possível adicionar uma assinatura não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   A assinatura é uma assinatura push.  
  
-   O Editor da publicação selecionada é o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior.  
  
 Clicar em **Adicionar assinante** mostra um menu com duas opções: **Adicionar assinante SQL Server** e **Adicionar assinante não-SQL Server**. Clique em **Adicionar assinante não-SQL Server** para adicionar um Oracle ou um assinante IBM DB2.  
  
 **Adicionar Assinante SQL Server**  
 Adicione um servidor à lista de servidores que podem ser habilitados como Assinantes. Esse botão é exibido quando uma ou mais das condições seguintes são verdadeiras:  
  
-   A publicação selecionada é uma publicação de mesclagem, de instantâneo ou transacional que não oferece suporte a assinaturas de atualização.  
  
-   A assinatura é uma assinatura pull.  
  
-   O Editor da publicação selecionada é anterior ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para versões anteriores, o botão só será exibido se uma ou mais das condições seguintes forem verdadeiras:  
  
    -   Você é um membro da função de servidor fixa **sysadmin** no Publicador.  
  
    -   O Assinante foi adicionado na página **Assinante** da caixa de diálogo **Propriedades do Publicador** .  
  
    -   A publicação permite assinaturas anônimas.  
  
## Consulte também  
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Assinantes não SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  