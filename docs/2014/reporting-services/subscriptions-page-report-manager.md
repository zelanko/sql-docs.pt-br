---
title: Página de assinaturas (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: cf3a6bd0-e0b2-4875-a532-63ef34cfa860
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eec92d7c58b68b14374666f65489f145fa863422
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66101084"
---
# <a name="subscriptions-page-report-manager"></a>Página Assinaturas (Gerenciador de Relatórios)
  Use a página Assinaturas para listar todas as assinaturas para o relatório atual ou fonte de dados compartilhada. Se você tiver permissão adequada (como a contida na tarefa "Gerenciar todas as assinaturas"), você poderá exibir as assinaturas de todos os usuários. Caso contrário, essa página só mostrará as assinaturas que você possui.  
  
> [!NOTE]  
>  Outras páginas também contêm informações de assinatura. Para obter mais informações, consulte [página Minhas assinaturas &#40;Gerenciador de relatórios&#41; ](../../2014/reporting-services/my-subscriptions-page-report-manager.md) para acessar todas as suas assinaturas em um único local ou o [página nova assinatura ou Editar assinatura &#40;Gerenciador de relatórios&#41; ](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md) para criar ou editar uma assinatura.  
  
 Algumas opções só são visíveis se houver assinaturas existentes com as quais é possível trabalhar. Se nenhuma assinatura estiver definida e você estiver acessando essa página de um relatório, **Nova Assinatura** e **Nova Assinatura Orientada por Dados** serão as únicas opções na página.  
  
 Antes de criar uma nova assinatura, você deve verificar se a fonte de dados do relatório armazena credenciais. Use a página de propriedades da Fonte de Dados para armazenar credenciais. Para obter mais informações, consulte [página de propriedades de fontes de dados &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md).  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
### <a name="to-open-the-subscriptions-page-for-report"></a>Para abrir a página Assinaturas do relatório  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório para o qual você deseja exibir ou configurar uma assinatura.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do relatório.  
  
4.  Selecione a guia **Assinaturas** .  
  
## <a name="options"></a>Opções  
 **Delete (excluir)**  
 Clique para excluir uma assinatura. Antes de excluir uma assinatura, marque a caixa de seleção ao lado de cada assinatura que você deseja excluir.  
  
 **Nova assinatura**  
 Clique para criar uma nova assinatura para o relatório atual. Esse botão é habilitado quando o relatório usa credenciais armazenadas ou nenhuma credencial. Esse botão não está disponível quando você abre a página Assinaturas para uma fonte de dados compartilhada.  
  
 **Nova assinatura controlada por dados**  
 Clique para gerar uma lista de assinantes e opções de entrega de um comando ou uma consulta em um repositório de dados que contenha essas informações. Esse botão é habilitado quando o relatório usa credenciais armazenadas ou nenhuma credencial. Esse botão não está disponível quando você abre a página Assinaturas para uma fonte de dados compartilhada.  
  
 **Editar**  
 Clique para exibir ou editar a descrição.  
  
 **Relatório**  
 Quando você abre essa página a partir de uma fonte de dados compartilhada, essa coluna identifica o relatório para o qual a assinatura é definida. A coluna **Pasta** identifica o local do relatório.  
  
 **Descrição**  
 Mostra uma descrição da assinatura.  
  
 **Gatilho**  
 Identifica critérios que causam a execução da assinatura. Um gatilho **TimedSubscription** é baseado em uma agenda que define quando a assinatura é executada. Um gatilho **SnapshotUpdated** é baseado em uma atualização de um instantâneo de relatório.  
  
 **Proprietário**  
 Exibe o nome do usuário que criou a assinatura.  
  
 **Última Execução**  
 Exibe a última vez em que a assinatura foi processada.  
  
 **Status**  
 Exibe o status da assinatura. Geralmente, o valor do status é Novo ou a data e hora da última execução da assinatura.  
  
 Um valor de status "Dados Incorretos" ocorre quando a assinatura inclui um ponteiro para valores criptografados que não são mais válidos (ou seja, para as credenciais armazenadas usadas para executar o relatório). Valores criptografados existentes se tornam inutilizáveis quando as chaves simétricas usadas para criptografar e descriptografar dados são recriadas no servidor de relatórios.  
  
 Uma assinatura não poderá ser processada se tiver sido desativada. Para atualizar a assinatura e torná-la operacional, abra e depois salve a assinatura.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Criar, modificar e excluir assinaturas padrão &#40;Reporting Services no modo nativo&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Criar, modificar e excluir agendas](subscriptions/create-modify-and-delete-schedules.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
