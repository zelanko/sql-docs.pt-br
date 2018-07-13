---
title: Criar, modificar e excluir assinaturas padrão (Reporting Services no modo nativo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
caps.latest.revision: 46
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a8c38acc8b25853db76bf89008189928c4cef578
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230386"
---
# <a name="create-modify-and-delete-standard-subscriptions-reporting-services-in-native-mode"></a>Create, Modify, and Delete Standard Subscriptions (Reporting Services in Native Mode)
  A assinatura padrão é criada por usuários individuais que desejam entregar um relatório por email ou em uma pasta compartilhada. Uma assinatura padrão sempre é definida pelo relatório no qual se baseia.  
  
 Um usuário que cria uma assinatura possui essa assinatura. Cada usuário pode modificar ou excluir as assinaturas que possui.  
  
> [!NOTE]  
>  Começando com [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] você pode transferir a propriedade de uma assinatura programaticamente. Não há nenhuma interface do usuário que você possa usar para transferir propriedade de assinaturas. Para obter mais informações, consulte <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 Dependendo da **rsreportserver. config** configurações do arquivo de configuração, os usuários podem até conseguir adicionar mais usuários a uma assinatura (por exemplo, um gerente adiciona os endereços de email ou seus relatórios diretos para que cada um receba uma cópia das relatório). O suporte a esse recurso depende da visibilidade do campo Para: durante a definição de assinaturas individuais. Para obter mais informações, consulte [configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Este tópico fornece informações sobre assinaturas padrão que são criadas e gerenciadas por usuários individuais. As assinaturas controladas por dados têm requisitos e etapas diferentes e são discutidas em um tópico separado. Para obter mais informações, consulte [criar, modificar e excluir uma assinatura controlada por dados](data-driven-subscriptions.md).  
  
 Neste tópico:  
  
-   [Para criar uma assinatura](#bkmk_create_subscription)  
  
-   [Para criar uma assinatura de compartilhamento de arquivo](#bkmk_create_fileshare_subscription)  
  
-   [Para criar uma assinatura de email](#bkmk_create_email_subscription)  
  
-   [Para modificar uma assinatura](#bkmk_modify_subscription)  
  
-   [Para excluir uma assinatura](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> Para criar uma assinatura  
 Para criar uma assinatura, escolha a ferramenta e a abordagem que são válidas para a implantação do servidor de relatório:  
  
-   O conteúdo neste tópico explica como criar assinaturas em um servidor de relatório do modo nativo usando o Gerenciador de Relatório da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Após definir uma assinatura, você poderá acessá-la no Gerenciador de Relatórios através da página Minhas Assinaturas ou da guia **Assinaturas** de um relatório específico.  
  
-   [Criar e gerenciar assinaturas de servidores de relatório de modo do SharePoint](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) explica como usar as páginas do aplicativo em um site do SharePoint para assinar relatórios em um servidor de relatório que é executado no modo integrado do SharePoint.  
  
 Este tópico fornece instruções para criar uma assinatura de email e uma assinatura de entrega de compartilhamento de arquivos.  
  
-   Para usar a entrega de email, o servidor de relatório deve ser configurado para uma conexão de gateway ou de servidor SMTP antes de criar a assinatura.  
  
-   Para usar a entrega de compartilhamento de arquivos, a pasta de destino já deve estar definida. Para obter mais informações, consulte [configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Antes de assinar um relatório, a fonte de dados do relatório deve estar configurada para usar credenciais armazenadas ou nenhuma credencial. Para obter mais informações, consulte [Store credenciais em uma fonte de dados do Reporting Services](../report-data/store-credentials-in-a-reporting-services-data-source.md). Caso contrário, o botão **Nova Assinatura** não estará disponível.  
  
 Este tópico não explica como criar uma assinatura controlada por dados. Para obter instruções sobre como criar uma assinatura controlada por dados, consulte [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md) ou a Ajuda online da página Criar uma Assinatura Controlada por Dados no Gerenciador de Relatórios.  
  
###  <a name="bkmk_create_fileshare_subscription"></a> Para criar uma assinatura de compartilhamento de arquivo  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  No Gerenciador de Relatórios, na página **Conteúdo** , navegue até o relatório que deseja assinar. Clique no relatório para abri-lo.  
  
3.  Clique na guia **Assinaturas** e, em seguida, clique em **Nova Assinatura**.  
  
4.  Em **Entregue por**, selecione **Compartilhamento de Arquivos do Windows**.  
  
5.  Em **Nome do Arquivo**, digite um nome de arquivo para o relatório.  
  
6.  Selecione **Adicionar uma extensão de arquivo quando o arquivo é criado**. Esta opção adiciona uma extensão de arquivo de três caracteres ao nome do arquivo. A extensão de arquivo é determinada pelo formato de saída do relatório selecionado.  
  
7.  No **caminho** texto, digite um caminho de convenção de nomenclatura Universal (UNC) para uma pasta existente onde você deseja entregar os relatórios (por exemplo, \\ \\< servername\>\\< myreports\>). Inclua caracteres de barra invertida dupla no começo do caminho. Não especifique barras invertidas à direita.  
  
8.  Em Formato de Processamento, selecione um formato de saída de relatório para entrega de arquivo. Escolha um formato que corresponda ao aplicativo de desktop que será usado para abrir o relatório. Evite formatos que não renderizam um relatório em um único fluxo ou que introduzam interatividade não compatível com um arquivo estático (por exemplo, HTML 4.0).  
  
9. Nas caixas de texto **Nome de usuário** e **Senha**, especifique as credenciais necessárias para acessar o compartilhamento de arquivos, usando o formato *\<domain>*\\*\<user name>* para o nome de usuário.  
  
10. Especifique opções de substituição. Se você clicar em **Não substituir o arquivo se existir uma versão anterior**, a entrega não ocorrerá caso um arquivo existente seja detectado. Se você clicar em **Incrementar nomes de arquivos quando versões mais recentes são adicionadas**, o servidor de relatório adicionará um número ao nome do arquivo para diferenciá-lo dos arquivos existentes com o mesmo nome.  
  
11. Especifique quando deseja que o relatório seja entregue:  
  
    -   Para agendar um horário de entrega, clique em **Quando a execução do relatório agendado estiver concluída** e clique no botão **Selecionar Agendamento** . Uma página de agenda é exibida.  
  
    -   Para selecionar uma agenda compartilhada predefinida que já tenha a data, a hora e as informações de recorrência que deseja usar, clique em **Em uma agenda compartilhada**e, em seguida, selecione a agenda a ser usada.  
  
    -   Para entregar o relatório quando um instantâneo de relatório for atualizado com uma versão mais recente, clique em**Quando o conteúdo do relatório for atualizado**. Se estiver assinando um relatório que recupera dados em intervalos agendados, a agenda usada para atualizar os dados determinará quando a assinatura será processada.  
  
        > [!NOTE]  
        >  Esta opção só está disponível para instantâneos que já estão associados a uma agenda de atualização.  
  
12. Para relatórios parametrizados, especifique os parâmetros a serem usados para o relatório dessa assinatura. Os parâmetros podem ser diferentes dos utilizados para executar o relatório sob demanda ou em outras operações agendadas.  
  
 O relatório é entregue como um arquivo estático. Se o relatório incluir recursos interativos (por exemplo, links para linhas e colunas adicionais), esses recursos não estarão disponíveis.  
  
###  <a name="bkmk_create_email_subscription"></a> Para criar uma assinatura de email  
  
1.  No Gerenciador de Relatórios, na página **Conteúdo** , navegue até o relatório que deseja assinar. Clique no relatório para abri-lo.  
  
2.  Clique na guia **Assinaturas** e, em seguida, clique em **Nova Assinatura**.  
  
3.  Na **entregues pelo**, selecione **email**. Se este tipo de entrega não estiver disponível, isso indica que o servidor de relatório não foi configurado para assinatura de email.  
  
4.  No **To** caixa de texto, o nome do destinatário no campo para: campo é autoendereçado usando sua conta de usuário de domínio. Definições de configuração do servidor de relatório determinam se o **para** campo é autoendereçado com sua conta de usuário. Para obter mais informações sobre como alterar os endereços de email de definições de configuração, consulte [configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
    > [!NOTE]  
    >  Dependendo de suas permissões, você pode digitar o endereço de email no qual deseja entregar o relatório. Para especificar vários endereços de email, separe-os com um ponto-e-vírgula (;). Você também pode digitar endereços de email adicionais nas caixas de texto **Cc**, **Cco**e **Responder** . Você precisa ter permissão para gerenciar todas as assinaturas.  
  
5.  Selecione as opções de entrega do seguinte modo:  
  
    -   Para inserir ou anexar uma cópia do relatório, selecione **Incluir Relatório**. O formato do relatório é determinado pelo formato de renderização selecionado. Não escolha essa opção caso o tamanho do relatório ultrapasse o limite definido para seu sistema de emails.  
  
    -   Para incluir um link de URL para o relatório no corpo da mensagem de email, selecione **incluir Link**.  
  
    > [!NOTE]  
    >  Se você desmarcar as duas opções, somente o texto de notificação na linha Assunto será enviado.  
  
6.  Escolha um formato de renderização na caixa de listagem **Formato de Processamento** . Esta opção estará disponível se você selecionar **Incluir Relatório** para inserir ou anexar uma cópia do relatório.  
  
    -   Para inserir o relatório no corpo da mensagem de email, selecione **Arquivo Web**.  
  
    -   Para enviar o relatório como um anexo, escolha qualquer um dos outros formatos de renderização.  
  
7.  Selecione uma prioridade na caixa de listagem **Prioridade** . No [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, esta configuração define um sinalizador para o nível de importância da mensagem de email.  
  
8.  Especifique quando deseja que o relatório seja entregue:  
  
    -   Para agendar um horário de entrega, clique em **Quando a execução do relatório agendado estiver concluída** e clique em **Selecionar Agendamento**. Uma página de agenda é exibida.  
  
    -   Para selecionar uma agenda compartilhada predefinida que já tenha a data, a hora e as informações de recorrência que deseja usar, clique em **Em uma agenda compartilhada**e, em seguida, selecione a agenda a ser usada.  
  
    -   Para entregar o relatório quando um instantâneo de relatório for atualizado com uma versão mais recente, clique em**Quando o conteúdo do relatório for atualizado**. Se estiver assinando um relatório que recupera dados em intervalos agendados, a agenda usada para atualizar os dados determinará quando a assinatura será processada.  
  
    > [!NOTE]  
    >  Esta opção só está disponível para instantâneos que já estão associados a uma agenda de atualização.  
  
9. Para relatórios parametrizados, especifique os parâmetros a serem usados para o relatório dessa assinatura. Os parâmetros especificados podem ser diferentes dos utilizados para executar o relatório sob demanda ou em outras operações agendadas.  
  
##  <a name="bkmk_modify_subscription"></a> Para modificar uma assinatura  
 Você pode modificar uma assinatura em qualquer momento. Se uma assinatura for modificada enquanto estiver sendo processada, as configurações atualizadas serão usadas se forem salvas no banco de dados do servidor de relatório antes de a extensão de entrega receber os dados da assinatura. Caso contrário, as configurações existentes são usadas.  
  
 Para localizar uma assinatura, use a página **Minhas Assinaturas** ou exiba as definições de assinatura associadas a um relatório. Não é possível procurar as assinaturas diretamente, nem procurar uma assinatura baseada no nome do proprietário, em informações de gatilho, em informações de status, etc.  
  
 As assinaturas também podem ser modificadas ou excluídas por administradores de servidor de relatório.  
  
> [!NOTE]  
>  Um administrador de servidor de relatório não pode gerenciar a partir de um lugar todas as assinaturas individuais que estão sendo usadas em um servidor de relatório específico. No entanto, os administradores de servidor de relatório podem acessar cada assinatura individual para modificá-la ou excluí-la.  
  
##  <a name="bkmk_delete_subscription"></a> Para excluir uma assinatura  
 Para excluir uma assinatura”  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  No Gerenciador de Relatórios, clique em **Minhas Assinaturas** na barra de ferramentas global e navegue até a assinatura que deseja modificar ou excluir.  
  
3.  Se preferir, na guia **Assinaturas** de um relatório aberto, localize a assinatura que deseja modificar ou excluir. Execute um destes procedimentos:  
  
    1.  Para modificar uma assinatura, clique em **Editar**.  
  
    2.  Para excluir uma assinatura, marque a caixa de seleção próxima à assinatura e, em seguida, clique em **Excluir**.  
  
 Este tópico não explica como cancelar uma assinatura que esteja em processamento no servidor de relatórios. Para obter mais informações sobre como cancelar assinaturas, consulte [gerenciar um processo em execução](manage-a-running-process.md)  
  
 Se desejar cancelar uma assinatura e não conseguir localizá-la facilmente, anote o relatório que está recebendo e procure-a por nome. Ao acessar o relatório, você pode remover a si mesmo da assinatura. Se não conseguir localizar a assinatura, esta talvez seja uma assinatura controlada por dados. Para obter mais informações, entre em contato com o administrador do servidor de relatório.  
  
 Uma assinatura será excluída automaticamente se o relatório subjacente for excluído. Se uma assinatura for excluída enquanto estiver sendo processada, a assinatura parará se a operação de exclusão ocorrer antes de a extensão de entrega receber os dados da assinatura. Caso contrário, a assinatura continuará sendo processada.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e permissões](../security/tasks-and-permissions.md)   
 [Criar e gerenciar assinaturas de servidores de relatório do modo do SharePoint](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Criar e gerenciar assinaturas de servidores de relatório do modo nativo](../create-manage-subscriptions-native-mode-report-servers.md)   
 [Assinaturas controladas por dados](data-driven-subscriptions.md)   
 [Assinaturas e entrega de &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [O Gerenciador de relatórios &#40;modo nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Usar Minhas Assinaturas](use-my-subscriptions-native-mode-report-server.md)  
  
  
