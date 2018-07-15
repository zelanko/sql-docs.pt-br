---
title: Página Minhas assinaturas (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 491a85a3-f323-4155-a0a8-de2779899995
caps.latest.revision: 28
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5e973ec6a3c50c43f6ee6bdee4ecfd70f2e2c9b2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177613"
---
# <a name="my-subscriptions-page-report-manager"></a>Página Minhas Assinaturas (Gerenciador de Relatórios)
  Use a página Minhas Assinaturas para exibir todas as suas assinaturas em um lugar. Desta página, você pode acessar e modificar ou excluir qualquer assinatura que possui. Você só possui as assinaturas que cria. Você não pode acessar as de outros usuários nem pode acessar assinaturas que você usa, mas não possui (por exemplo, se seu nome foi adicionado a uma assinatura existente definida por outro usuário). Você não pode criar assinaturas nesta página. Para obter mais informações sobre como criar assinaturas, consulte o [página nova assinatura ou Editar assinatura &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md).  
  
 Por padrão, as assinaturas são classificadas em ordem alfabética pelo nome do relatório. Clique em um cabeçalho de coluna diferente para alterar o modo de classificação das assinaturas. Se você não tiver assinaturas ou se a permissão para criar ou gerenciar assinaturas estiver desabilitada, nenhuma assinatura será exibida na página.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
### <a name="to-open-the-my-subscriptions-page"></a>Para abrir a página Minhas Assinaturas  
  
1.  Abra o Gerenciador de Relatórios.  
  
2.  Na parte superior da página, no canto direito, clique em Minhas Assinaturas.  
  
    > [!NOTE]  
    >  A página Minhas Assinaturas está sempre disponível, mesmo que você não tenha permissão para criar assinaturas.  
  
## <a name="options"></a>Opções  
 **Delete (excluir)**  
 Marque a caixa de seleção ao lado de cada assinatura que você deseja excluir e clique em **Excluir**.  
  
 **Editar**  
 Clique para exibir ou editar a descrição.  
  
 **Relatório**  
 Mostra o relatório que é especificado na assinatura. Clique no nome do relatório para abri-lo.  
  
 **Descrição**  
 Mostra uma descrição da assinatura. Clique na descrição para exibir ou editar as informações de assinatura para o relatório.  
  
 **Pasta**  
 Exibe a pasta que contém o relatório especificado na assinatura. Clique no nome de pasta para exibir o conteúdo da pasta.  
  
 **Gatilho**  
 Identifica critérios que causam a execução da assinatura. Um gatilho **TimedSubscription** é baseado em uma agenda que define quando a assinatura é executada. Um gatilho **SnapshotUpdated** é baseado em uma atualização de um instantâneo de relatório.  
  
 **Última Execução**  
 Exibe a última vez em que a assinatura foi processada.  
  
 **Status**  
 Exibe o status da assinatura. Geralmente, o valor do status é "Novo" ou a data e hora da última execução da assinatura.  
  
 Um valor de status "Dados Incorretos" ocorre quando a assinatura inclui um ponteiro para valores criptografados que não são mais válidos (ou seja, para as credenciais armazenadas usadas para executar o relatório). Valores criptografados existentes se tornam inutilizáveis quando as chaves simétricas usadas para criptografar e descriptografar dados são recriadas no servidor de relatórios.  
  
 Uma assinatura não poderá ser processada se tiver sido desativada. Para atualizar a assinatura e torná-la operacional, abra e depois salve a assinatura.  
  
## <a name="see-also"></a>Consulte também  
 [Assinaturas e entrega de &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
