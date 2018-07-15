---
title: Publicador Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.selectoraclepublisher.f1
ms.assetid: 019b7c49-dcca-445d-8969-5982a8ccbc1a
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 38c361df88abf2435e920adaabc3039615c7d915
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223231"
---
# <a name="oracle-publisher"></a>Editor Oracle
  A partir do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite publicar dados de um banco de dados Oracle usando replicação de instantâneo e transacional. Para obter mais informações, consulte [Visão geral da publicação Oracle](non-sql/oracle-publishing-overview.md).  
  
 O Editor Oracle deve usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributor remoto; esse assistente deve ser executado no servidor depois que o software de rede Oracle necessário tiver sido instalado e testado. Para obter mais informações, consulte [Configure an Oracle Publisher](non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
> [!IMPORTANT]  
>  Se outro administrador tiver configurado o banco de dados Oracle como um Publicador, depois de clicar em **Avançar** você será solicitado a inserir a senha do logon de replicação usado para conectar-se ao banco de dados Oracle. O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criará um mapeamento entre seu logon e a conexão de servidor vinculado com o banco de dados Oracle. Você não será solicitado a inserir uma senha para conexões subsequentes com o banco de dados Oracle.  
  
## <a name="options"></a>Opções  
 **Publicadores Oracle**  
 Selecione um Editor Oracle na lista. Essa lista contém Editores Oracle que foram previamente configurados para usar o servidor no qual o assistente está sendo executado como Distribuidor. Se a lista estiver vazia ou o Editor Oracle que você quiser usar não estiver na lista, clique em **Adicionar Editor Oracle**.  
  
 **Adicionar Editor Oracle**  
 Clique para iniciar a caixa de diálogo **Propriedades do Distribuidor** . Nessa caixa de diálogo, clique em **Adicionar**e em **Adicionar Editor Oracle**. Na caixa de diálogo **Conectar ao Servidor** , especifique o nome do servidor Oracle, o logon e a senha para o esquema de usuário administrativo de replicação. Para obter mais informações, consulte [Conectar ao servidor &#40;Oracle&#41;, Logon](connect-to-server-oracle-login.md).  
  
> [!NOTE]  
>  Se o servidor no qual o assistente está sendo executado ainda não estiver configurado como Distribuidor, você será solicitado a configurá-lo agora.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma publicação de um Banco de Dados Oracle](publish/create-a-publication-from-an-oracle-database.md)   
 [Referência de propriedades &#40;Replicação&#41;](properties-reference-replication.md)  
  
  
