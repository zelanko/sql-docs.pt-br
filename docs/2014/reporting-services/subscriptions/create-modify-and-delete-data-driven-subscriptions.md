---
title: Criar, modificar e excluir uma assinatura controlada por dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 68a9d73139154ffd3d1343fb54a33ce103d6d7ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100937"
---
# <a name="create-modify-and-delete-a-data-driven-subscription"></a>Create, Modify, and Delete a Data-Driven Subscription
  Uma assinatura controlada por dados é uma assinatura com base em consulta que obtém os valores de dados usados para processar a assinatura em tempo de execução. Quando a assinatura é acionada, uma consulta é processada para obter informações atualizadas sobre destinatários, opções de entrega de relatórios, formatos de renderização e configurações de parâmetro. Os resultados da consulta são combinados com a definição da assinatura para criar uma assinatura dinâmica que usa os dados já mantidos em um banco de dados de funcionários, de clientes ou que contenha informações que podem ser usadas como dados do assinante.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo do SharePoint|  
  
 **Neste tópico:**  
  
-   [Criar e modificar uma assinatura controlada por dados](#bkmk_create_and_modify)  
  
-   [Definir uma consulta que recupera informações de assinatura](#bkmk_define_query)  
  
-   [Fazer uma assinatura](#bkmk_run_subscription)  
  
-   [Gerenciar e excluir uma assinatura controlada por dados](#bkmk_manage_and_delete)  
  
##  <a name="create-and-modify-a-data-driven-subscription"></a><a name="bkmk_create_and_modify"></a>Criar e modificar uma assinatura controlada por dados  
 Para criar uma nova assinatura controlada por dados ou modificar uma assinatura existente, use as páginas Criar Assinatura Controlada por Dados no Gerenciador de Relatórios. Essas páginas fazem com que você percorra cada etapa da criação ou modificação de uma assinatura. Para acessar uma assinatura depois de criá-la, use a página Minhas Assinaturas e a lista de Assinaturas de um relatório. Para saber como criar uma assinatura controlada por dados, consulte [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md).  
  
 Para criar uma assinatura controlada por dados, selecione um relatório que use credenciais armazenadas ou nenhuma credencial. Quando você criar a assinatura controlada por dados, considere o uso de uma convenção de nomenclatura para o campo de descrição, de modo que seja possível diferenciar facilmente as assinaturas padrão das assinaturas controladas por dados.  
  
#### <a name="to-create-a-data-driven-subscription-native-mode"></a>Para criar uma assinatura controlada por dados (Modo Nativo)  
  
1.  Em Report Manager navegue até a pasta que contém o relatório, focalize o relatório, abra o menu opções e clique em **gerenciar.**  
  
2.  Clique na guia **Assinaturas** .  
  
3.  Clique no botão **Nova Assinatura Controlada por Dados** .  
  
#### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>Para criar uma assinatura controlada por dados (Modo do SharePoint)  
  
1.  Na biblioteca de documentos do SharePoint, passe o mouse sobre o relatório, abra o menu de opções e clique em **Gerenciar Assinaturas**.  
  
2.  Clique em **Adicionar Assinatura Controlada por Dados**.  
  
#### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>Para modificar uma assinatura controlada por dados existente (Modo Nativo)  
  
1.  No Gerenciador de Relatórios, navegue até a pasta que contém o relatório, focalize o relatório, abra o menu de opções e clique em **Gerenciar**.  
  
2.  Clique na guia **assinaturas** . como alternativa, clique no link **minhas assinaturas** no parte superior do Gerenciador de relatórios  
  
3.  Selecione a assinatura que você deseja modificar. O ícone a seguir indica uma assinatura controlada por dados: ![ícone de assinatura controlada por dados](../media/hlp-16subscriptiondd.gif "Ícone de assinatura controlada por dados")  
  
#### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>Para modificar uma assinatura controlada por dados existente (Modo do SharePoint)  
  
1.  Na biblioteca de documentos do SharePoint, passe o mouse sobre o relatório, abra o menu de opções e clique em **Gerenciar Assinaturas**.  
  
2.  Selecione a assinatura que você deseja modificar.  
  
> [!NOTE]  
>  Você pode modificar qualquer valor que já esteja especificado. Todos os valores são apresentados como se eles tivessem sido criados primeiro, exceto pela senha que é usada para acessar o repositório de dados do assinante. Você deve digitar novamente a senha sempre que modificar os valores na segunda página ou em qualquer página subsequente.  
  
 Para criar uma assinatura controlada por dados, atenda aos seguintes requisitos:  
  
-   **Requisitos de relatório**. O relatório deve usar credenciais armazenadas ou nenhuma credencial para recuperar os dados durante a execução. Você não pode assinar um relatório que use credenciais não representadas ou delegadas para se conectar a uma fonte de dados externa; as credenciais do usuário que cria ou possui uma assinatura não estarão disponíveis quando a assinatura é processada. As credenciais armazenadas podem ser uma conta do Windows ou uma conta de usuário de banco de dados. Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
     Não é possível assinar um relatório do Construtor de Relatórios que use um modelo como uma fonte de dados e o modelo contiver configurações de segurança do item de modelo. Somente relatórios que usam a segurança do item de modelo são incluídos nesta restrição.  
  
     Você não pode criar uma assinatura controlada por dados em um relatório que contém a expressão `User!UserID` .  
  
-   **Requisitos de dados**. Você deve ter uma fonte de dados externa acessível que contenha dados de assinante.  
  
-   **Requisitos de usuário**. O autor da assinatura deve ter permissão para "Gerenciar relatórios" e "Gerenciar todas as assinaturas". Para obter mais informações sobre permissões de tarefa em nível de item, consulte [Tarefas e Permissões](../security/tasks-and-permissions.md). O autor também tem que ter as credenciais necessárias para acessar a fonte de dados externa que contém dados de assinante.  
  
##  <a name="define-a-query-that-retrieves-subscription-information"></a><a name="bkmk_define_query"></a>Definir uma consulta que recupera informações de assinatura  
 Uma assinatura controlada por dados deve especificar uma consulta ou um comando que recupere dados de assinante. A consulta deve produzir uma linha para cada assinante. Se você estiver usando a extensão de entrega de email, a consulta deverá retornar um alias de email válido para cada assinante. O número de entregas feitas se baseia no número de linhas retornadas pela consulta. Se o conjunto de linhas for composto por 10.000 linhas, a assinatura entregará 10.000 relatórios.  
  
 Se executar a consulta for uma tarefa demorada, você poderá aumentar o valor do tempo limite para acomodar outros processamentos.  
  
 Para esta etapa, a consulta deve ser validada a consulta antes de continuar. A validação não processa a consulta, mas ela retorna uma lista de todas as colunas que estão no conjunto de linhas para que você possa fazer referência a colunas nas seleções subsequentes. Se houver falha na validação da consulta, você não poderá continuar. Há uma falha na validação da consulta se a sintaxe da consulta estiver incorreta ou se a conexão com a fonte de dados não for válida. Use o botão **Voltar** para fazer correções na fonte de dados.  
  
##  <a name="run-a-subscription"></a><a name="bkmk_run_subscription"></a>Executar uma assinatura  
 Você configura as condições para o processamento da assinatura. Você pode configurar uma agenda ou pode disparar a assinatura para coincidir com as atualizações para um instantâneo de execução do relatório.  
  
 ![Observação](../media/rs-fyinote.png "observação") Embora não haja nenhum recurso na interface do usuário que você possa usar para executar imediatamente uma assinatura, você pode usar um script simples do Windows PowerShell para disparar a execução de uma assinatura. Para obter mais informações, consulte a seção "script: executar (acionar) uma única assinatura" [em usar o PowerShell para alterar e listar Reporting Services proprietários de assinatura e executar uma assinatura](manage-subscription-owners-and-run-subscription-powershell.md).  
  
 Agenda e condições para execução de assinaturas controladas por dados é o mesmo que processamento para assinaturas padrão.  
  
##  <a name="manage-and-delete-a-data-driven-subscription"></a><a name="bkmk_manage_and_delete"></a>Gerenciar e excluir uma assinatura controlada por dados  
 Uma assinatura controlada por dados que está em andamento não pode ser interrompida nem excluída pela página Gerenciar Trabalhos do Gerenciador de Relatórios. Por esse motivo, é vantajoso usar uma agenda compartilhada para acionar a assinatura controlada por dados. Dessa forma, se quiser impedir temporariamente o processamento de uma assinatura, poderá fazer uma pausa na agenda que aciona a assinatura. Para saber mais, consulte [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../create-manage-subscriptions-native-mode-report-servers.md).  
  
 Para excluir uma assinatura controlada por dados, selecione-a na página Minhas Assinaturas ou na página Assinaturas de um relatório e clique em **Excluir**.  
  
 Para obter instruções sobre como cancelar uma assinatura controlada por dados, consulte [Gerenciar um processo em execução](manage-a-running-process.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar, modificar e excluir assinaturas padrão &#40;Reporting Services no modo nativo&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../create-manage-subscriptions-native-mode-report-servers.md)   
 [Página de assinaturas &#40;Report Manager&#41;](../subscriptions-page-report-manager.md)   
 [Página Minhas Assinaturas &#40;Gerenciador de Relatórios&#41;](../my-subscriptions-page-report-manager.md)  
  
  
