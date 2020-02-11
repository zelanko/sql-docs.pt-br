---
title: Segurança do Agente de Mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.MA.f1
helpviewer_keywords:
- Merge Agent Security dialog box
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: af3d3490957114d6ba7731b49435dc7e90122f90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62932491"
---
# <a name="merge-agent-security"></a>Segurança do Merge Agent
  A caixa de diálogo **agente de mesclagem segurança** permite que você especifique [!INCLUDE[msCoName](../../includes/msconame-md.md)] a conta do Windows na qual o agente de mesclagem é executado. O Merge Agent é executado no Distribuidor para assinaturas push e no Assinante para assinaturas pull. A conta do Windows também é conhecida como a *conta de processo*, porque o processo do agente é executado nessa conta. Opções adicionais disponíveis na caixa de diálogo dependem de como você a acessa:  
  
-   Se a caixa de diálogo for acessada do Assistente para Nova Assinatura, também permitirá que você especifique o contexto no qual o Merge Agent fará conexões com o Assinante (para assinaturas push) ou com o Publicador e o Distribuidor (para assinaturas pull). A conexão pode ser feita usando a conta do Windows ou sob o contexto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma conta que você especificar.  
  
-   Se a caixa de diálogo for acessada pela caixa de diálogo **Propriedades da Assinatura** , especifique o contexto no qual o Merge Agent fará conexões ao clicar no botão de propriedades (**...**) na linha **Conexão do Assinante** ou **Conexão do Publicador** daquela caixa de diálogo. Para obter mais informações sobre como acessar a caixa de diálogo **Propriedades da Assinatura**, consulte [Exibir e modificar as propriedades da assinatura push](view-and-modify-push-subscription-properties.md) e [Exibir e modificar as propriedades da assinatura pull](view-and-modify-pull-subscription-properties.md).  
  
 Todas as contas devem ser válidas, com a senha correta especificada para cada conta. Contas e senhas não são validadas até que um agente seja executado.  
  
## <a name="options"></a>Opções  
 **Conta de processo**  
 Insira uma conta Windows na qual o Merge Agent é executado.  
  
-   Para assinaturas push, a conta deve:  
  
    -   No mínimo, seja um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.  
  
    -   Ser um membro da PAL.  
  
    -   Ser um logon associado a um usuário no banco de dados de publicação.  
  
    -   Ter permissões de leitura no compartilhamento de instantâneo.  
  
-   Para assinaturas pull, a conta deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de assinatura.  
  
 Serão requeridas permissões adicionais se a conta do processo for representada quando as conexões forem feitas. Consulte as seções **Conectar ao Publicador e ao Distribuidor** e **Conectar ao Assinante** a seguir.  
  
 **A conta de processo** não pode ser especificada para assinaturas [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]pull no, porque o agente de mesclagem não é executado em instâncias [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]do.  
  
 **Senha** e **Confirmar senha**  
 Insira a senha para a conta do Windows.  
  
 **Conectar-se ao Publicador e ao distribuidor**  
 Para assinaturas push, as conexões com o Publicador e o Distribuidor são sempre feitas representando a conta especificada na caixa de texto **Conta do processo** .  
  
 Para assinaturas pull, selecione se o Merge Agent deve fazer conexões com o Publicador e o Distribuidor representando a conta especificada na caixa de texto **Conta do processo** ou usando uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda a seleção para representar a conta do Windows em vez de usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para a conexão deve:  
  
-   Ser um membro da PAL.  
  
-   Ser um logon associado a um usuário no banco de dados de publicação.  
  
-   Ser um logon associado a um usuário no banco de dados de distribuição (o usuário pode ser o usuário Convidado).  
  
-   Ter permissões de leitura no compartilhamento de instantâneo.  
  
 **Conectar-se ao Assinante**  
 Para assinaturas pull, as conexões com o Assinante são sempre feitas representando a conta especificada na caixa de texto **Conta do processo** .  
  
 Para assinaturas push, selecione se o Merge Agent deve fazer conexões com o Publicador e o Distribuidor representando a conta especificada na caixa de texto **Conta do processo** ou usando uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  É recomendável a seleção para representar a conta do Windows em vez de usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para conexão com o Assinante deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar logons e senhas na replicação](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Modelo de segurança do agente de replicação](security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação](agents/replication-agents-overview.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Assinar publicações](subscribe-to-publications.md)  
  
  
