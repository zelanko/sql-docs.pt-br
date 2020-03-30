---
title: Criar e gerenciar assinaturas de servidores de relatório no modo Nativo | Microsoft Docs
ms.date: 05/28/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5bcfeabda2eda62a6a4118ac5542e83a4b0afd66
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76971310"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>Crie e gerencie assinaturas de servidores de relatório no modo Nativo
  A assinatura padrão é criada por usuários individuais que desejam entregar um relatório por email ou em uma pasta compartilhada. Este tópico fornece informações sobre assinaturas padrão que são criadas e gerenciadas por usuários individuais. As assinaturas controladas por dados têm requisitos e etapas diferentes e são discutidas em um tópico separado. Para obter mais informações, consulte [Criar, modificar e excluir assinaturas controladas por dados](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)  
  
 **Neste artigo:**  
  
-   [Requisitos gerais para assinaturas](#bkmk_create_subscription)  
  
-   [Para criar uma assinatura de compartilhamento de arquivo](#bkmk_create_fileshare_subscription)  
  
-   [Para criar uma assinatura de email](#bkmk_create_email_subscription)  
  
-   [Para modificar uma assinatura](#bkmk_modify_subscription)  
  
-   [Para excluir uma assinatura](#bkmk_delete_subscription)  
  
##  <a name="general-requirements-for-subscriptions"></a><a name="bkmk_create_subscription"></a> Requisitos gerais para assinaturas  
 O conteúdo deste artigo explica como criar assinaturas em um servidor de relatório do modo nativo usando o portal da Web em [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Após definir uma assinatura, você poderá acessá-la no portal da Web por meio da página Minhas Assinaturas ou da guia **Assinaturas** de um relatório específico.  
  
 [Criar e gerenciar assinaturas de servidores de relatório no modo SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) explica como usar as páginas de aplicativo em um site do SharePoint para assinar relatórios em um servidor de relatório em modo do SharePoint.  
  
-   Para usar a entrega de email, o servidor de relatório deve ser configurado para uma conexão de gateway ou de servidor SMTP antes de criar a assinatura. Para obter mais informações, consulte [Entrega de email no Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   Para usar a entrega de compartilhamento de arquivos, uma pasta de destino já deve estar definida. Para saber mais, confira [Configurações de Assinatura e uma Conta de Compartilhamento de Arquivos (Configuration Manager)](../install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md).  
  
 Antes de assinar um relatório, a fonte de dados do relatório deve estar configurada para usar credenciais armazenadas ou nenhuma credencial. Para obter mais informações, consulte [Armazenar credenciais em uma fonte de dados do Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md). Caso contrário, o botão **Nova Assinatura** não estará disponível.  
  
 Este artigo não explica como criar uma assinatura controlada por dados. Para obter instruções sobre como criar uma assinatura controlada por dados, confira [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md).  
  
## <a name="to-create-a-file-share-subscription"></a><a name="bkmk_create_fileshare_subscription"></a> Para criar uma assinatura de compartilhamento de arquivo  
  
1. Navegue até o [portal da Web de um servidor de relatório (Modo Nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
2.  Navegue até o relatório desejado. Clique com botão direito do mouse no relatório e selecione **Assinar**.  
  
3.  **Descrição**: digite uma descrição para a assinatura do relatório com no máximo 512 caracteres.  
  
4.  **Proprietário**: o proprietário do campo usa como padrão o usuário atual e não pode ser editado quando você cria a assinatura. No entanto, depois que a assinatura é salva, você pode alterar as propriedades da assinatura incluindo o proprietário e a descrição.  

5. Em **Tipo de assinatura**, selecione o botão de opção **Assinatura padrão**.

6. Na seção **Agendamento**, selecione:  
   - **Agenda compartilhada**.  
   - **Informar agenda específica**.  

    Para saber mais sobre agendamento, confira [Agendamentos](../../reporting-services/subscriptions/schedules.md).
  
7. Em **Destino**, selecione **Compartilhamento de arquivos do Windows**.  
  
8. Em **Opções de entrega (compartilhamento de arquivos do Windows)** , especifique:  
   - **Nome do Arquivo**: digite um nome de arquivo para o relatório.
   - **Adicionar uma extensão de arquivo quando o arquivo é criado**: essa opção adiciona uma extensão de arquivo de três caracteres ao nome do arquivo. A extensão de arquivo é determinada pelo formato de saída do relatório selecionado.  
   - **Caminho**: digite um caminho UNC para uma pasta existente na qual você deseja entregar os relatórios (por exemplo, \\<nomedoservidor\>\<meusrelatórios>). Inclua caracteres de barra invertida dupla no começo do caminho. Não especifique barras invertidas à direita.  
  
     ![assinatura do compartilhamento de arquivo](../../reporting-services/subscriptions/media/create-and-manage-subscriptions-for-native-mode-report-servers/subscription-file-share-delivery-option.png "assinatura do compartilhamento de arquivo")  
  
   - **Formato de Renderização**: selecione um formato de saída de relatório para entrega de arquivo. Escolha um formato que corresponda ao aplicativo de desktop que será usado para abrir o relatório. Evite formatos que não renderizam um relatório em um único fluxo ou que introduzam interatividade não compatível com um arquivo estático (por exemplo, HTML 4.0).  
  
   - **Credenciais**: selecione para usar a conta de compartilhamento de arquivos ou uma credencial de usuário específica do Windows. O **Usar conta de compartilhamento de arquivos** estará desabilitado se o administrador de relatórios não tiver configurado uma conta de compartilhamento de arquivos. Para obter mais informações, consulte [Configurações de Assinatura e uma Conta de Compartilhamento de Arquivos &#40;Gerenciador de Configurações&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md). Nas caixas de texto **Nome de usuário** e **Senha**, especifique as credenciais necessárias para acessar o compartilhamento de arquivos, usando o formato *\<domain>* \\ *\<user name>* para o nome de usuário.  
  
   - **Opções de substituição**:  
     - **Substituir um arquivo existente com uma versão mais recente**.  
     - **Não substituir o arquivo se existir uma versão anterior**, a entrega não ocorrerá se um arquivo existente for detectado.  
     - **Incrementar nomes de arquivos quando versões mais recentes são adicionadas**, o servidor de relatório adicionará um número ao nome do arquivo para diferenciá-lo dos arquivos existentes com o mesmo nome.  

9. Para relatórios parametrizados, especifique os parâmetros a serem usados para o relatório dessa assinatura. Os parâmetros podem ser diferentes dos utilizados para executar o relatório sob demanda ou em outras operações agendadas.  
  
O relatório é entregue como um arquivo estático. Se o relatório incluir recursos interativos (por exemplo, links para linhas e colunas adicionais), esses recursos não estarão disponíveis.  
  
##  <a name="to-create-an-e-mail-subscription"></a><a name="bkmk_create_email_subscription"></a> Para criar uma assinatura de email  
  
1. Navegue até o [portal da Web de um servidor de relatório (Modo Nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
2. Navegue até o relatório desejado. Clique com botão direito do mouse no relatório e selecione **Assinar**.  
  
3. **Descrição**: digite uma descrição para a assinatura do relatório com no máximo 512 caracteres.  
  
4.  **Proprietário**: o proprietário do campo usa como padrão o usuário atual e não pode ser editado quando você cria a assinatura. No entanto, depois que a assinatura é salva, você pode alterar as propriedades da assinatura incluindo o proprietário e a descrição.  

5. Em **Tipo de assinatura**, selecione o botão de opção **Assinatura padrão**.

6. Na seção **Agendamento**, selecione:  
   - **Agenda compartilhada**.  
   - **Informar agenda específica**.  

    Para saber mais sobre agendamento, confira [Agendamentos](../../reporting-services/subscriptions/schedules.md).
  
7. Em **Destino**, selecione **Email**.  Se a opção **Email** não estiver disponível, isso indicará que o servidor de relatório não foi configurado para assinaturas de email. Confira [Configurar o email para um aplicativo de serviço Reporting Services](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md).
  
8. Em **Opções de entrega (email)** , especifique:
   - **Para**: o nome do destinatário no campo Para: é autoendereçado usando sua conta de usuário de domínio. Verifique se o formato é [nome do usuário]@[domínio.com]. As configurações do servidor de relatório determinam se o campo **Para** é endereçado a si mesmo com sua conta de usuário. Para saber mais sobre como alterar os endereços de email de definições de configuração, confira [Configurar o email para um aplicativo de serviço do Reporting Services](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)

     >[!NOTE]  
     > Dependendo de suas permissões, você pode digitar o endereço de email no qual deseja entregar o relatório. Para especificar vários endereços de email, separe-os com um ponto-e-vírgula (;). Você também pode digitar endereços de email adicionais nas caixas de texto **Cc**, **Cco**e **Responder** . Você precisa ter permissão para gerenciar todas as assinaturas.  
  
   - **Assunto**: usa como padrão "@ReportName foi executado em @ExecutionTime". Você pode editar o assunto, mas observe que o @ReportName e @ExecutionTime são as únicas variáveis globais com suporte no campo **Assunto**.  
  
     ![assinatura de email](../../reporting-services/subscriptions/media/create-and-manage-subscriptions-for-native-mode-report-servers/subscription-e-mail-delivery-option.png "assinatura de email")  

   - **Incluir Relatório**: selecione esta opção para inserir ou anexar uma cópia do relatório. O formato do relatório é determinado pelo formato de renderização selecionado. Não escolha essa opção caso o tamanho do relatório ultrapasse o limite definido para seu sistema de emails.  
  
   - **Incluir Link**: selecione esta opção para incluir um link de URL no relatório, no corpo da mensagem de email.  
  
     >[!NOTE]  
     >Se você desmarcar as duas opções, somente o texto de notificação na linha Assunto será enviado.  
  
   - Escolha um formato de renderização na caixa de listagem **Formato de Processamento** . Esta opção estará disponível se você selecionar **Incluir Relatório** para inserir ou anexar uma cópia do relatório.  
      - Para inserir o relatório no corpo da mensagem de email, selecione **MHTML (arquivo da Web)** .  
      - Para enviar o relatório como um anexo, escolha qualquer um dos outros formatos de renderização.  
  
   - Selecione uma prioridade na caixa de listagem **Prioridade** . No [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, esta configuração define um sinalizador para o nível de importância da mensagem de email.  
   - Insira um **Comentário**, se desejar.
  
9. Para relatórios parametrizados, especifique os parâmetros a serem usados para o relatório dessa assinatura. Os parâmetros especificados podem ser diferentes dos utilizados para executar o relatório sob demanda ou em outras operações agendadas.  
  
##  <a name="to-modify-a-subscription"></a><a name="bkmk_modify_subscription"></a> Para modificar uma assinatura  
 Você pode modificar uma assinatura em qualquer momento. Se uma assinatura for modificada enquanto estiver sendo processada, as configurações atualizadas serão usadas se forem salvas no servidor de relatório antes de a extensão de entrega receber os dados da assinatura. Caso contrário, as configurações existentes são usadas.  
  
 Um usuário que cria uma assinatura possui essa assinatura. Cada usuário pode modificar ou excluir as assinaturas que possui. Você pode alterar o proprietário do relatório na página de propriedades de assinatura ou pode alterar a propriedade programaticamente. Para saber mais, consulte o seguinte:  
  
-   [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 Para localizar uma assinatura, use a página **Minhas Assinaturas** ou exiba as definições de assinatura associadas a um relatório. Não é possível procurar as assinaturas diretamente, nem procurar uma assinatura baseada no nome do proprietário, em informações de gatilho, em informações de status, etc.  
  
 As assinaturas também podem ser modificadas ou excluídas por administradores de servidor de relatório.  
  
>[!NOTE]  
> Um administrador de servidor de relatório não pode gerenciar a partir de um lugar todas as assinaturas individuais que estão sendo usadas em um servidor de relatório específico. No entanto, os administradores de servidor de relatório podem acessar cada assinatura individual para modificá-la ou excluí-la.  
  
##  <a name="to-delete-a-subscription"></a><a name="bkmk_delete_subscription"></a> Para excluir uma assinatura  
Para excluir uma assinatura:  
  
1. Navegue até o [portal da Web de um servidor de relatório (Modo Nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
2. No portal da Web, selecione **Minhas Assinaturas** na barra de ferramentas e navegue até a assinatura que deseja modificar ou excluir.  
  
3. Clique com botão direito do mouse no relatório e selecione **Excluir**.  
  
Para cancelar uma assinatura atualmente em processamento no servidor de relatórios, consulte [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
 Se desejar cancelar uma assinatura e não conseguir localizá-la, anote o relatório que está recebendo e pesquise pelo seu nome. Ao acessar o relatório, você pode remover a si mesmo da assinatura. Se não conseguir localizar a assinatura, esta talvez seja uma assinatura controlada por dados. Para obter mais informações, entre em contato com o administrador do servidor de relatório.  
  
 Uma assinatura será excluída automaticamente se o relatório subjacente for excluído. Se uma assinatura for excluída enquanto estiver sendo processada, a assinatura parará se a operação de exclusão ocorrer antes de a extensão de entrega receber os dados da assinatura. Caso contrário, a assinatura continuará sendo processada.  
  
## <a name="see-also"></a>Confira também  
 [Criar e gerenciar assinaturas de servidores de relatório no modo SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
 [Assinaturas controladas por dados](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
 [O portal da Web de um servidor de relatório (modo nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)  
 [Usar Minhas Assinaturas &#40;Servidor de Relatório no modo Nativo&#41;](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
