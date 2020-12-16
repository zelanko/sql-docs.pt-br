---
description: Publicadores
title: Assinantes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.subscribers.f1
helpviewer_keywords:
- Subscribers [SQL Server replication]
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: be8ccf0bbaf2efa80c9b0e48e39a0743d63b0c75
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479607"
---
# <a name="subscribers"></a>Publicadores
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  Especifique os Assinantes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que receberão uma assinatura para a publicação selecionada.


[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opções  
 **Publicadores**  
 Marque a caixa de seleção na grade para habilitar a fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente como um Assinante da publicação escolhida na página **Publicação**. Se o Assinante não estiver na lista, clique em **Adicionar Assinante** ou **Adicionar Assinante SQL Server**.  
  
 **Banco de dados de assinatura**  
 As informações exibidas e as informações exibidas nessa coluna dependem do tipo de Assinante listado na coluna **Assinantes** :  
  
-   Para Assinantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selecione um banco de dados de assinatura da lista **Banco de Dados de Assinatura** para criar um novo banco de dados selecionando o comando **Novo banco de dados** na mesma lista.  
  
    > [!NOTE]  
    >  Se você estiver habilitando o Publicador como um Assinante, o banco de dados de assinatura deverá ser diferente do banco de dados de publicação.  
  
-   Para Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o banco de dados de assinatura não é exibido. Especifique o banco de dados, juntamente com outras informações de conexão, no campo **Nome da fonte de dados** da caixa de diálogo **Adicionar não SQL Server** . Essa caixa de diálogo está disponível clicando em **Adicionar Assinante** e depois clicando em **Adicionar Assinante não SQL Server**.  
  
 **Adicionar Assinante**  
 Adicione um servidor à lista de servidores que podem ser habilitados como Assinantes. Esse botão é exibido quando todas as condições seguintes são verdadeiras:  
  
-   A publicação selecionada é uma publicação de instantâneo ou transacional que não oferece suporte a assinaturas de atualização.  
  
    > [!NOTE]  
    >  Se a publicação que você estiver assinando tiver assinaturas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a publicação ainda não tiver sido habilitada como Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não será possível adicionar uma assinatura não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   A assinatura é uma assinatura push.  
  
-   O Publicador da publicação selecionada é o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior.  
  
 Clicar em **Adicionar Assinante** mostra um menu com duas opções: **Adicionar Assinante SQL Server** e **Adicionar Assinante não SQL Server**. Clique em **Adicionar Assinante não SQL Server** para adicionar um Assinante Oracle ou IBM DB2.  
  
 **Adicionar Assinante SQL Server**  
 Adicione um servidor à lista de servidores que podem ser habilitados como Assinantes. Esse botão é exibido quando uma ou mais das condições seguintes são verdadeiras:  
  
-   A publicação selecionada é uma publicação de mesclagem, de instantâneo ou transacional que não oferece suporte a assinaturas de atualização.  
  
-   A assinatura é uma assinatura pull.  
  
-   O Editor da publicação selecionada é anterior ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para versões anteriores, o botão só será exibido se uma ou mais das condições seguintes forem verdadeiras:  
  
    -   Você é um membro da função de servidor fixa **sysadmin** no Publicador.  
  
    -   O Assinante foi adicionado na página **Assinante** da caixa de diálogo **Propriedades do Publicador** .  
  
    -   A publicação permite assinaturas anônimas.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
