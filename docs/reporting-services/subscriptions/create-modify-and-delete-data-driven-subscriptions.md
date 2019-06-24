---
title: Criar, modificar e excluir assinaturas controladas por dados | Microsoft Docs
ms.date: 06/12/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b385e04cf2efa103dba4a66d4e794a7984814fb4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67140263"
---
# <a name="create-modify-and-delete-data-driven-subscriptions"></a>Criar, modificar e excluir assinaturas controladas por dados
  Uma assinatura controlada por dados é uma assinatura com base em consulta que obtém os valores de dados usados para processar a assinatura em tempo de execução. Quando a assinatura é acionada, uma consulta é processada para obter informações atualizadas sobre destinatários, opções de entrega de relatórios, formatos de renderização e configurações de parâmetro. Os resultados da consulta são combinados com a definição da assinatura para criar uma assinatura dinâmica que usa os dados já mantidos em um banco de dados de funcionários, de clientes ou que contenha informações que podem ser usadas como dados do assinante.  
  
 Para criar uma nova assinatura controlada por dados ou modificar uma assinatura existente, use o **Manage** > **assinaturas** página no portal da web. O **assinaturas** página percorre cada etapa da criação ou modificação de uma assinatura. Para acessar uma assinatura depois de criá-la, use a página **Minhas Assinaturas** e a lista de Assinaturas de um relatório. Para saber como criar uma assinatura controlada por dados, consulte [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md).  
  
 Neste artigo:  
  
-   [Gerenciar e excluir uma assinatura controlada por dados](#bkmk_manage_and_delete)  
  
-   [Criar e modificar uma assinatura controlada por dados](#bkmk_create_and_modify)  
  
-   [Definir uma consulta que recupera informações de assinatura](#bkmk_define_query)  
  
-   [Executar a assinatura](#bkmk_run_subscription)  
  
##  <a name="bkmk_manage_and_delete"></a> Gerenciar e excluir uma assinatura controlada por dados  
 Uma assinatura controlada por dados que está em andamento não pode ser interrompida ou excluída por meio do portal da web. Por esse motivo, é vantajoso usar uma agenda compartilhada para acionar a assinatura controlada por dados. Dessa forma, se quiser impedir temporariamente o processamento de uma assinatura, poderá fazer uma pausa na agenda que aciona a assinatura. Para saber mais, consulte [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
 Para excluir uma assinatura controlada por dados, marque a caixa de seleção ao lado do relatório sobre o **assinaturas** página e, em seguida, selecione **excluir**.  
  
 Para obter instruções sobre como cancelar uma assinatura controlada por dados, consulte [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
##  <a name="bkmk_create_and_modify"></a> Criar e modificar uma assinatura controlada por dados  
 Para criar uma assinatura controlada por dados, selecione um relatório que use credenciais armazenadas ou nenhuma credencial. Quando você criar a assinatura controlada por dados, considere o uso de uma convenção de nomenclatura para o campo de descrição, de modo que seja possível diferenciar facilmente as assinaturas padrão das assinaturas controladas por dados.  
  
### <a name="to-create-a-data-driven-subscription-native-mode"></a>Para criar uma assinatura controlada por dados (Modo Nativo)  
  
1. No portal da web, navegue até a pasta que contém o relatório, clique com botão direito do relatório e selecione **gerenciar** no menu suspenso.  
  
2. Selecione a guia **Assinaturas** .  
  
3. Selecione **+ nova assinatura** sobre o **assinaturas** página.  
  
### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>Para criar uma assinatura controlada por dados (Modo do SharePoint)  
  
1. Na biblioteca de documentos do SharePoint, passe o mouse sobre o relatório, abra o menu de opções e clique em **Gerenciar Assinaturas**.  
  
2. Clique em **Adicionar Assinatura Controlada por Dados**.  
  
### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>Para modificar uma assinatura controlada por dados existente (Modo Nativo)  
  
1. No portal da web, navegue até a pasta que contém o relatório, clique com botão direito do relatório e selecione **gerenciar** no menu suspenso.  
  
2. Selecione a guia **Assinaturas** .  
  
3. Marque a caixa de seleção próxima à assinatura que você deseja modificar e, em seguida, selecione **editar**. Assinaturas controladas por dados terá o valor "controlada por dados" no **tipo** coluna.  
  
### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>Para modificar uma assinatura controlada por dados existente (Modo do SharePoint)  
  
1.  Na biblioteca de documentos do SharePoint, passe o mouse sobre o relatório, abra o menu de opções e clique em **Gerenciar Assinaturas**.  
  
2.  Selecione a assinatura que você deseja modificar.  
  
    > [!NOTE]  
    > Você pode modificar qualquer valor que já esteja especificado. Todos os valores são apresentados como se eles tivessem sido criados primeiro, exceto pela senha que é usada para acessar o repositório de dados do assinante. Você deve digitar novamente a senha sempre que modificar os valores na segunda página ou em qualquer página subsequente.  
  
  Para criar uma assinatura controlada por dados, atenda aos seguintes requisitos:  
  
-   **Requisitos de relatório**. O relatório deve usar credenciais armazenadas ou nenhuma credencial para recuperar os dados durante a execução. Você não pode assinar um relatório que use credenciais não representadas ou delegadas para se conectar a uma fonte de dados externa; as credenciais do usuário que cria ou possui uma assinatura não estarão disponíveis quando a assinatura é processada. As credenciais armazenadas podem ser uma conta do Windows ou uma conta de usuário de banco de dados. Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
     Não é possível assinar um relatório do Construtor de Relatórios que use um modelo como uma fonte de dados e o modelo contiver configurações de segurança do item de modelo. Somente relatórios que usam a segurança do item de modelo são incluídos nesta restrição.  
  
     Você não pode criar uma assinatura controlada por dados em um relatório que contém a expressão `User!UserID` .  
  
-   **Requisitos de dados**. Você deve ter uma fonte de dados externa acessível que contenha dados de assinante.  
  
-   **Requisitos de usuário**. O autor da assinatura deve ter permissão para "Gerenciar relatórios" e "Gerenciar todas as assinaturas". Para obter mais informações sobre permissões de tarefa em nível de item, consulte [Tarefas e Permissões](../../reporting-services/security/tasks-and-permissions.md). O autor também tem que ter as credenciais necessárias para acessar a fonte de dados externa que contém dados de assinante.  
  
##  <a name="bkmk_define_query"></a> Definir uma consulta que recupera informações de assinatura  
 Uma assinatura controlada por dados deve especificar uma consulta ou um comando que recupere dados de assinante. A consulta deve produzir uma linha para cada assinante. Se você estiver usando a extensão de entrega de email, a consulta deverá retornar um alias de email válido para cada assinante. O número de entregas feitas se baseia no número de linhas retornadas pela consulta. Se o conjunto de linhas for composto por 10.000 linhas, a assinatura entregará 10.000 relatórios.  
  
 Se executar a consulta for uma tarefa demorada, você poderá aumentar o valor do tempo limite para acomodar outros processamentos.  
  
 Para esta etapa, a consulta deve ser validada a consulta antes de continuar. A validação não processa a consulta, mas ela retorna uma lista de todas as colunas que estão no conjunto de linhas para que você possa fazer referência a colunas nas seleções subsequentes. Se houver falha na validação da consulta, você não poderá continuar. Há uma falha na validação da consulta se a sintaxe da consulta estiver incorreta ou se a conexão com a fonte de dados não for válida. Use o botão **Voltar** para fazer correções na fonte de dados.  
  
##  <a name="bkmk_run_subscription"></a> Executar a assinatura  
 Você deve especificar condições para processar a assinatura. Você pode especificar uma agenda ou pode acionar a assinatura para coincidir com as atualizações para um instantâneo de execução do relatório. O processamento de assinaturas controladas por dados é o mesmo que o processamento para assinaturas padrão.  
  
## <a name="see-also"></a>Confira também  
 [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [O portal da Web de um servidor de relatório (modo nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Trabalhando com assinaturas (portal da web)](../../reporting-services/working-with-subscriptions-web-portal.md) [usar Minhas assinaturas (servidor de relatório de modo nativo)](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 