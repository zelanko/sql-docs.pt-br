---
title: 'Lição 3: Definindo uma assinatura controlada por dados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ee51a19d1dc169d2ae784d8a44403e021ff8b665
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108506"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>Lesson 3: Defining a Data-Driven Subscription
  Nesta lição, você vai usar as páginas da assinatura controlada por dados para se conectar a uma fonte de dados de assinatura, criar uma consulta que recupera dados de assinatura e mapear o conjunto de resultados para opções de relatório e entrega.  
  
> [!NOTE]  
>  Antes de começar, verifique se o serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent está em execução. Se não estiver, não será possível salvar a assinatura.  
  
 Esta lição pressupõe que você concluiu a Lição 1 e Lição 2, e que a fonte de dados de relatório usa credenciais armazenadas.  Para obter mais informações, consulte [Lição 2: modificando as propriedades da fonte de dados do relatório](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  
  
 Neste tópico:  
  
-   [Iniciar o assistente de assinatura controlada por dados](#bkmk_startwizard)  
  
-   [Etapa 1 - Definir uma descrição](#bkmk_definesubscription)  
  
-   [Etapa 2 - Definir uma conexão com a fonte de dados de assinante](#bkmk_defineconnectiontosubscriber)  
  
-   [Etapa 3 - Definir uma consulta para recuperar dados de assinante](#bkmk_definequery)  
  
-   [Etapa 4 - Definir opções de entrega](#bkmk_set_deliveryoptions)  
  
-   [Etapa 5 - Configurar um valor de parâmetro para variar a saída de relatório](#bkmk_configure_parameter)  
  
-   [Etapa 6 - Para agendar uma assinatura](#bkmk_schedule_subscription)  
  
##  <a name="start-the-data-driven-subscription-wizard"></a><a name="bkmk_startwizard"></a>Iniciar o assistente de assinatura controlada por dados  
  
1.  No Gerenciador de Relatórios, clique em **Página Inicial**e navegue até a pasta que contém o relatório **Pedidos de Vendas** .  
  
2.  No menu de contexto do relatório, clique em **Gerenciar**e clique na guia **Assinaturas** .  
  
3.  Clique em **nova assinatura voltada para dados**. Se este botão não estiver visível, você não tem permissões do Gerenciador de Conteúdo.  
  
##  <a name="step-1---define-a-description"></a><a name="bkmk_definesubscription"></a>Etapa 1 – definir uma descrição  
  
1.  Digite **Entrega de ordem de venda** na descrição.  
  
2.  Selecione **Compartilhamento de Arquivos do Windows** para **Especifique como os destinatários devem ser notificados**.  
  
3.  Selecione **Especificar apenas para essa assinatura**e clique em **Avançar**.  
  
##  <a name="step-2---define-a-connection-to-the-subscriber-data-source"></a><a name="bkmk_defineconnectiontosubscriber"></a>Etapa 2 – definir uma conexão com a fonte de dados do assinante  
  
1.  Selecione **Microsoft SQL Server** como o tipo de fonte de dados.  
  
2.  Em Cadeia de conexão, digite a seguinte cadeia de conexão:  
  
    ```  
    data source=localhost; initial catalog=Subscribers  
    ```  
  
    > [!NOTE]  
    >  Os assinantes são o banco de dados que você criou na lição 1.  
  
3.  Clique em **Credenciais armazenadas com segurança no servidor de relatórios**.  
  
4.  Em **Nome de Usuário** e **Senha**, digite seu nome de usuário de domínio e senha. Inclua a conta de domínio e de usuário ao especificar **Nome de Usuário**.  
  
    > [!NOTE]  
    >  As credenciais usadas para a conexão com uma fonte de dados de assinante não são retransmitidas para o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Se você modificar a assinatura mais tarde, deverá digitar novamente a senha usada para a conexão com a fonte de dados.  
  
5.  Selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados**e, em seguida, clique em **Avançar**.  
  
##  <a name="step-3---define-a-query-to-retrieve-subscriber-data"></a><a name="bkmk_definequery"></a>Etapa 3 – definir uma consulta para recuperar dados do assinante  
  
1.  Na caixa de consulta, digite a seguinte consulta:  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  Especifique um tempo limite de 30 segundos.  
  
3.  Clique em **Validar**e, em seguida, clique em **Avançar**.  
  
##  <a name="step-4---set-delivery-options"></a><a name="bkmk_set_deliveryoptions"></a>Etapa 4 – definir opções de entrega  
  
1.  Em **Nome de arquivo**, selecione **Obtenha o valor no banco de dados**. Selecione o campo **Pedido**.  
  
2.  Para **Caminho**, selecione **Especifique um valor estático**. Em Definindo Valor, digite o nome de um compartilhamento de arquivos públicos para os quais você tem permissões de gravação (por exemplo, `\\mycomputer\public\myreports`).  
  
3.  Em **Formato de Renderização**, selecione **Obtenha o valor no banco de dados**. Selecione **Formato**.  
  
4.  Em **Modo de gravação**, selecione **Especifique um valor estático** e selecione **Incrementação automática**.  
  
5.  Em **Extensão de Arquivo**, selecione **Especifique um valor estático** e selecione **Verdadeiro**.  
  
6.  Em **Nome de usuário**, selecione **Especifique um valor estático**. Digite sua conta de usuário de domínio. Insira neste formato: `<domain>\<account>`. A conta de usuário precisa ter permissões para o caminho que você configurou nas etapas anteriores.  
  
7.  Em **Senha**, selecione **Especifique um valor estático**. Digite sua senha. Digite a senha com cuidado. O assistente não valida a senha.  
  
8.  Clique em **Avançar**.  
  
##  <a name="step-5---configure-a-parameter-value-to-very-report-output"></a><a name="bkmk_configure_parameter"></a>Etapa 5 – configurar um valor de parâmetro para saída de relatório muito  
  
1.  Em **OrderNumber**, selecione **Obtenha o valor no banco de dados**. Em Valor, selecione **Pedido**. Clique em **Avançar**.  
  
##  <a name="step-6---to-schedule-a-subscription"></a><a name="bkmk_schedule_subscription"></a>Etapa 6 – para agendar uma assinatura  
  
1.  Clique em **Em um agendamento criado para esta assinatura**e, em seguida, clique em **Avançar**.  
  
2.  Em **Detalhes do Agendamento**, clique em **Uma vez**.  
  
3.  Especifique uma hora de início que esteja alguns minutos adiantados da hora atual.  
  
4.  Clique em **Concluir**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Quando a assinatura é executada, quatro arquivos de relatórios são entregues no compartilhamento de arquivos especificado, um para cada pedido na fonte de dados *Assinantes* . Cada entrega deve ser exclusiva em termos de dados (os dados devem ser específicos do pedido), formato de renderização e formato de arquivo. Você pode abrir cada relatório da pasta compartilhada para verificar se cada versão está personalizada com base nas opções de assinatura definidas.  
  
 ![Lista de arquivos criados pela assinatura](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-filelist.gif "Lista de arquivos criados pela assinatura")  
  
 A página de assinatura no Gerenciador de Relatórios conterá a data da **Última Execução** e o **Status** da assinatura.  
  
> [!NOTE]  
>  Atualize a página depois que a assinatura for executada para consultar as informações atualizadas.  
  
 ![Resultados da assinatura no Gerenciador de Relatórios](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.gif "Resultados da assinatura no Gerenciador de Relatórios")  
  
 Esta etapa conclui o tutorial “Definindo uma assinatura controlada por dados”. Para saber mais sobre outros [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] tutoriais, consulte [Reporting Services tutoriais &#40;&#41;do SSRS ](../reporting-services/reporting-services-tutorials-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [Criar, modificar e excluir uma assinatura controlada por dados](subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
