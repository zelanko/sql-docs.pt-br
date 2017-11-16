---
title: Publicador Oracle | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.selectoraclepublisher.f1
ms.assetid: 019b7c49-dcca-445d-8969-5982a8ccbc1a
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d847ec3d684ed015a526e239f27b66b169734c6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="oracle-publisher"></a>Editor Oracle
  A partir do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite publicar dados de um banco de dados Oracle usando replicação de instantâneo e transacional. Para obter mais informações, consulte [Visão geral da publicação Oracle](../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
 O Editor Oracle deve usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributor remoto; esse assistente deve ser executado no servidor depois que o software de rede Oracle necessário tiver sido instalado e testado. Para obter mais informações, consulte [Configure an Oracle Publisher](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
> [!IMPORTANT]  
>  Se outro administrador tiver configurado o banco de dados Oracle como um Publicador, depois de clicar em **Avançar** você será solicitado a inserir a senha do logon de replicação usado para conectar-se ao banco de dados Oracle. O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criará um mapeamento entre seu logon e a conexão de servidor vinculado com o banco de dados Oracle. Você não será solicitado a inserir uma senha para conexões subsequentes com o banco de dados Oracle.  
  
## <a name="options"></a>Opções  
 **Publicadores Oracle**  
 Selecione um Editor Oracle na lista. Essa lista contém Editores Oracle que foram previamente configurados para usar o servidor no qual o assistente está sendo executado como Distribuidor. Se a lista estiver vazia ou o Editor Oracle que você quiser usar não estiver na lista, clique em **Adicionar Editor Oracle**.  
  
 **Adicionar Editor Oracle**  
 Clique para iniciar a caixa de diálogo **Propriedades do Distribuidor** . Nessa caixa de diálogo, clique em **Adicionar**e em **Adicionar Editor Oracle**. Na caixa de diálogo **Conectar ao Servidor** , especifique o nome do servidor Oracle, o logon e a senha para o esquema de usuário administrativo de replicação. Para obter mais informações, consulte [Conectar ao servidor &#40;Oracle&#41;, Logon](../../relational-databases/replication/connect-to-server-oracle-login.md).  
  
> [!NOTE]  
>  Se o servidor no qual o assistente está sendo executado ainda não estiver configurado como Distribuidor, você será solicitado a configurá-lo agora.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma publicação de um Banco de Dados Oracle](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)   
 [Referência de propriedades &#40;Replicação&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
