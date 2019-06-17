---
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 508abbeac89bb374fbfb68e368e68988218e0e91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62521821"
---
# <a name="subscribers"></a>Publicadores
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Especifique os Assinantes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que receberão uma assinatura para a publicação selecionada.  
  
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
  
-   O Editor da publicação selecionada é o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior.  
  
 Ao clicar em **Adicionar Assinante**, será mostrado um menu com duas opções: **Adicionar Assinante do SQL Server** e **Adicionar Assinante não SQL Server**. Clique em **Adicionar Assinante não SQL Server** para adicionar um Assinante Oracle ou IBM DB2.  
  
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
  
  
