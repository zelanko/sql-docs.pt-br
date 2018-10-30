---
title: Criar, modificar e excluir assinaturas controladas por dados | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 533391424ab1eeacb52d59e56070f0b874320942
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50030385"
---
# <a name="create-modify-and-delete-data-driven-subscriptions"></a>Criar, modificar e excluir assinaturas controladas por dados
  Uma assinatura controlada por dados é uma assinatura com base em consulta que obtém os valores de dados usados para processar a assinatura em tempo de execução. Quando a assinatura é acionada, uma consulta é processada para obter informações atualizadas sobre destinatários, opções de entrega de relatórios, formatos de renderização e configurações de parâmetro. Os resultados da consulta são combinados com a definição da assinatura para criar uma assinatura dinâmica que usa os dados já mantidos em um banco de dados de funcionários, de clientes ou que contenha informações que podem ser usadas como dados do assinante.  
  
 Para criar uma nova assinatura controlada por dados ou modificar uma assinatura existente, use as páginas Criar Assinatura Controlada por Dados no Gerenciador de Relatórios. Essas páginas fazem com que você percorra cada etapa da criação ou modificação de uma assinatura. Para acessar uma assinatura depois de criá-la, use a página Minhas Assinaturas e a lista de Assinaturas de um relatório. Para saber como criar uma assinatura controlada por dados, consulte [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md).  
  
 Neste tópico:  
  
-   [Gerenciando e excluindo uma assinatura controlada por dados](#bkmk_manage_and_delete)  
  
-   [Criando e modificando uma assinatura controlada por dados](#bkmk_create_and_modify)  
  
-   [Definindo uma consulta que recupera informações de assinatura](#bkmk_define_query)  
  
-   [Executando a assinatura](#bkmk_run_subscription)  
  
##  <a name="bkmk_manage_and_delete"></a> Gerenciando e excluindo uma assinatura controlada por dados  
 Uma assinatura controlada por dados que está em andamento não pode ser interrompida nem excluída pela página Gerenciar Trabalhos do Gerenciador de Relatórios. Por esse motivo, é vantajoso usar uma agenda compartilhada para acionar a assinatura controlada por dados. Dessa forma, se quiser impedir temporariamente o processamento de uma assinatura, poderá fazer uma pausa na agenda que aciona a assinatura. Para saber mais, consulte [old_Criar e gerenciar assinaturas de servidores de relatório no modo Nativo](https://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b).  
  
 Para excluir uma assinatura controlada por dados, selecione-a na página Minhas Assinaturas ou na página Assinaturas de um relatório e clique em **Excluir**.  
  
 Para obter instruções sobre como cancelar uma assinatura controlada por dados, consulte [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
##  <a name="bkmk_create_and_modify"></a> Criando e modificando uma assinatura controlada por dados  
 Para criar uma assinatura controlada por dados, selecione um relatório que use credenciais armazenadas ou nenhuma credencial. Quando você criar a assinatura controlada por dados, considere o uso de uma convenção de nomenclatura para o campo de descrição, de modo que seja possível diferenciar facilmente as assinaturas padrão das assinaturas controladas por dados.  
  
#### <a name="to-create-a-data-driven-subscription-native-mode"></a>Para criar uma assinatura controlada por dados (Modo Nativo)  
  
1.  No Gerenciador de Relatórios, navegue até a pasta que contém o relatório, focalize o relatório, abra o menu de opções e clique em **Gerenciar**.  
  
2.  Clique na guia **Assinaturas** .  
  
3.  Clique no botão **Nova Assinatura Controlada por Dados** .  
  
#### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>Para criar uma assinatura controlada por dados (Modo do SharePoint)  
  
1.  Na biblioteca de documentos do SharePoint, passe o mouse sobre o relatório, abra o menu de opções e clique em **Gerenciar Assinaturas**.  
  
2.  Clique em **Adicionar Assinatura Controlada por Dados**.  
  
#### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>Para modificar uma assinatura controlada por dados existente (Modo Nativo)  
  
1.  No Gerenciador de Relatórios, navegue até a pasta que contém o relatório, focalize o relatório, abra o menu de opções e clique em **Gerenciar**.  
  
2.  Clique na guia **Assinaturas** . Como alternativa, clique no link **Minhas Assinaturas** na parte superior do gerenciador de relatórios  
  
3.  Selecione a assinatura que você deseja modificar. O seguinte ícone indica uma assinatura controlada por dados: ![ícone da assinatura controlada por dados](../../reporting-services/subscriptions/media/hlp-16subscriptiondd.gif "ícone da assinatura controlada por dados")  
  
#### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>Para modificar uma assinatura controlada por dados existente (Modo do SharePoint)  
  
1.  Na biblioteca de documentos do SharePoint, passe o mouse sobre o relatório, abra o menu de opções e clique em **Gerenciar Assinaturas**.  
  
2.  Selecione a assinatura que você deseja modificar.  
  
> [!NOTE]  
>  Você pode modificar qualquer valor que já esteja especificado. Todos os valores são apresentados como se eles tivessem sido criados primeiro, exceto pela senha que é usada para acessar o repositório de dados do assinante. Você deve digitar novamente a senha sempre que modificar os valores na segunda página ou em qualquer página subsequente.  
  
 Para criar uma assinatura controlada por dados, atenda aos seguintes requisitos:  
  
-   **Requisitos de relatório**. O relatório deve usar credenciais armazenadas ou nenhuma credencial para recuperar os dados durante a execução. Você não pode assinar um relatório que use credenciais não representadas ou delegadas para se conectar a uma fonte de dados externa; as credenciais do usuário que cria ou possui uma assinatura não estarão disponíveis quando a assinatura é processada. As credenciais armazenadas podem ser uma conta do Windows ou uma conta de usuário de banco de dados. Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
     Não é possível assinar um relatório do Construtor de Relatórios que use um modelo como uma fonte de dados e o modelo contiver configurações de segurança do item de modelo. Somente relatórios que usam a segurança do item de modelo são incluídos nesta restrição.  
  
     Você não pode criar uma assinatura controlada por dados em um relatório que contém a expressão `User!UserID` .  
  
-   **Requisitos de dados**. Você deve ter uma fonte de dados externa acessível que contenha dados de assinante.  
  
-   **Requisitos de usuário**. O autor da assinatura deve ter permissão para "Gerenciar relatórios" e "Gerenciar todas as assinaturas". Para obter mais informações sobre permissões de tarefa em nível de item, consulte [Tarefas e Permissões](../../reporting-services/security/tasks-and-permissions.md). O autor também tem que ter as credenciais necessárias para acessar a fonte de dados externa que contém dados de assinante.  
  
##  <a name="bkmk_define_query"></a> Definindo uma consulta que recupera informações de assinatura  
 Uma assinatura controlada por dados deve especificar uma consulta ou um comando que recupere dados de assinante. A consulta deve produzir uma linha para cada assinante. Se você estiver usando a extensão de entrega de email, a consulta deverá retornar um alias de email válido para cada assinante. O número de entregas feitas se baseia no número de linhas retornadas pela consulta. Se o conjunto de linhas for composto por 10.000 linhas, a assinatura entregará 10.000 relatórios.  
  
 Se executar a consulta for uma tarefa demorada, você poderá aumentar o valor do tempo limite para acomodar outros processamentos.  
  
 Para esta etapa, a consulta deve ser validada a consulta antes de continuar. A validação não processa a consulta, mas ela retorna uma lista de todas as colunas que estão no conjunto de linhas para que você possa fazer referência a colunas nas seleções subsequentes. Se houver falha na validação da consulta, você não poderá continuar. Há uma falha na validação da consulta se a sintaxe da consulta estiver incorreta ou se a conexão com a fonte de dados não for válida. Use o botão **Voltar** para fazer correções na fonte de dados.  
  
##  <a name="bkmk_run_subscription"></a> Executando a assinatura  
 Você deve especificar condições para processar a assinatura. Você pode especificar uma agenda ou pode acionar a assinatura para coincidir com as atualizações para um instantâneo de execução do relatório. O processamento de assinaturas controladas por dados é o mesmo que o processamento para assinaturas padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [old_Criar e gerenciar assinaturas de servidores de relatório no modo Nativo](https://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)   
 [Página Assinaturas &#40;Gerenciador de Relatórios&#41;](https://msdn.microsoft.com/library/cf3a6bd0-e0b2-4875-a532-63ef34cfa860)   
 [Página Minhas Assinaturas &#40;Gerenciador de Relatórios&#41;](https://msdn.microsoft.com/library/491a85a3-f323-4155-a0a8-de2779899995)  
  
  
