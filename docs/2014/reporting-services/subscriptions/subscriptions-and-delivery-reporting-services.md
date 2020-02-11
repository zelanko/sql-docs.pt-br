---
title: Assinaturas e entrega (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- reports [Reporting Services], distributing
- distributing reports [Reporting Services]
- published reports [Reporting Services], distributing
- sending reports
- sharing reports
- delivering reports [Reporting Services]
- distributing reports [Reporting Services], subscriptions
- subscriptions [Reporting Services], about subscriptions
- subscriptions [Reporting Services]
ms.assetid: be7ec052-28e2-4558-bc09-8479e5082926
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f598946ec6231d1ca5edacf1810431beb4638f88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100668"
---
# <a name="subscriptions-and-delivery-reporting-services"></a>Assinaturas e entrega (Reporting Services)
  Uma assinatura do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] é uma configuração que fornece um relatório em um momento específico ou em resposta a um evento, em um formato de arquivo que você especificar. Por exemplo, toda quarta-feira, salvar o relatório MonthlySales.rdl como um documento do Microsoft Word em um compartilhamento de arquivo. As assinaturas podem ser usadas para agendar e automatizar a entrega de um relatório e com um conjunto específico de valores de parâmetros do relatório.  
  
 Você pode criar várias assinaturas para um único relatório e variar as opções de assinatura. Por exemplo, você pode especificar valores de parâmetros diferentes para produzir três versões de um relatório, como um relatório de vendas da região Ocidental, da região Oriental e de todas as vendas.  
  
 ![exemplo de fluxo de assinatura ssrs](../media/ssrs-subscription-example-flow.png "exemplo de fluxo de assinatura ssrs")  
  
 As assinaturas não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
> [!NOTE]
>  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] A partir do, você pode transferir a propriedade de uma assinatura programaticamente. Não há nenhuma interface do usuário que você possa usar para transferir propriedade de assinaturas. Para obter mais informações, <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>consulte e [usar o PowerShell para alterar e listar Reporting Services proprietários de assinatura e executar uma assinatura](manage-subscription-owners-and-run-subscription-powershell.md).  
  
 **Neste tópico:**  
  
-   [Cenários de assinatura e entrega](#bkmk_subscription_scenarios)  
  
-   [Assinaturas baseadas em dados e padrão](#bkmk_standard_and_datadriven)  
  
-   [Requisitos de assinatura](#bkmk_subscription_requirements)  
  
-   [Extensões de Entrega](#bkmk_delivery_extensions)  
  
-   [Partes de uma assinatura](#bkmk_parts_of_subscription)  
  
-   [Como as assinaturas são processadas](#bkmk_subscription_processing)  
  
-   [Como as assinaturas são processadas](#bkmk_subscription_processing)  
  
 **Tópicos nesta seção:**  
  
-   [Entrega de email no Reporting Services](e-mail-delivery-in-reporting-services.md) Descreve a operação e a configuração de entrega de email do servidor de relatório.  
  
-   [Entrega de compartilhamento de arquivos no Reporting Services](file-share-delivery-in-reporting-services.md) Descreve a configuração e a operação de entrega de compartilhamento de arquivos do servidor de relatório.  
  
-   [Entrega de biblioteca do SharePoint no Reporting Services](sharepoint-library-delivery-in-reporting-services.md) Descreve a entrega de assinatura para uma biblioteca do SharePoint.  
  
-   [Assinaturas controladas por dados](data-driven-subscriptions.md) Fornece informações sobre como usar assinaturas controladas por dados para personalizar a saída do relatório em tempo de execução.  
  
-   [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../create-manage-subscriptions-native-mode-report-servers.md)  
  
-   [Criar e gerenciar assinaturas de servidores de relatório no modo SharePoint](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
-   [Monitorar assinaturas do Reporting Services](monitor-reporting-services-subscriptions.md)  
  
-   [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](manage-subscription-owners-and-run-subscription-powershell.md)  
  
##  <a name="bkmk_subscription_scenarios"></a>Cenários de assinatura e entrega  
 Para cada assinatura, você pode configurar opções de entrega, e as opções disponíveis são determinadas pela extensão de entrega escolhida. Uma extensão de entrega é um módulo que dá suporte a alguma maneira de distribuição. 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui várias extensões de entrega. Também a extensão de entrega que pode estar disponível por outros fornecedores.  
  
 Se você for um desenvolvedor, poderá criar extensões de entrega personalizadas para oferecer suporte a mais cenários. Para obter mais informações, consulte [Implementing a Delivery Extension](../extensions/delivery-extension/implementing-a-delivery-extension.md).  
  
 A tabela a seguir descreve os cenários comuns de assinatura do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .  
  
|Cenário|DESCRIÇÃO|  
|--------------|-----------------|  
|Relatórios de email|Relatórios de email a usuários individuais e grupos. Crie uma assinatura e especifique um alias de grupo ou de email para receber um relatório que queira distribuir. Você pode fazer com que o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] determine os dados da assinatura em tempo de execução. Se você quiser enviar o mesmo relatório a um grupo que tenha uma lista mutante de membros, poderá usar uma consulta para derivar a lista de assinaturas em tempo de execução.|  
|Exibir os relatórios offline|Os relatórios que você deseja arquivar podem ser enviados diretamente a uma pasta compartilhada cujo backup é feito em uma agenda noturna. Relatórios grandes cujo carregamento é muito demorado em um navegador podem ser enviados a uma pasta compartilhada em um formato que pode ser exibido em um aplicativo de área de trabalho. Você pode selecionar um dos seguintes formatos para a saída de assinatura:<br /><br /> Arquivo XML com dados de relatório<br /><br /> CSV (delimitado por vírgulas)<br /><br /> PDF<br /><br /> MHTML (arquivo da Web)<br /><br /> Microsoft Excel<br /><br /> Arquivo TIFF<br /><br /> Microsoft Word|  
|Cache pré-carregado|Se você tiver várias instâncias de um relatório com parâmetros ou um grande número de usuários de relatório que veem relatórios, será possível pré-carregar os relatórios no cache para reduzir o tempo de processamento necessário para exibição dos mesmos.|  
|Relatórios voltados para dados|Use assinaturas controladas por dados para personalizar a saída do relatório, as opções de entrega e as configurações de parâmetro de relatório em tempo de execução. A assinatura usa uma consulta para obter valores de entrada de uma fonte de dados em tempo de execução. Você pode usar assinaturas controladas por dados para executar uma operação de mesclagem de email que envia um relatório para uma lista de assinantes determinada no momento em que a assinatura é processada.|  
  
##  <a name="bkmk_standard_and_datadriven"></a>Assinaturas baseadas em dados e padrão  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]dá suporte a dois tipos de assinaturas: **Standard** e **controlada por dados**. Assinaturas padrão são criadas e gerenciadas por usuários individuais. Uma assinatura padrão consiste em valores estáticos que não podem ser variados durante o processamento da assinatura. Para cada assinatura padrão há exatamente um conjunto de opções de apresentação de relatório, opções de entrega e parâmetros de relatório.  
  
 Assinaturas controladas por dados obtêm informações de assinatura em tempo de execução consultando a fonte de dados externa que fornece valores usados para especificar um destinatário, parâmetros de relatório ou um formato do aplicativo. Você pode usar assinaturas controladas por dados se tiver uma lista de destinatários muito grande ou desejar variar a saída de relatório para cada destinatário. Para usar assinaturas controladas por dados, é necessário ter conhecimento especializado na criação de consultas e entender como os parâmetros são usados. Administradores de servidor de relatório geralmente criam e administram essas assinaturas. Para saber mais, consulte o seguinte:  
  
-   [Assinaturas controladas por dados](data-driven-subscriptions.md)  
  
-   [Criar uma assinatura controlada por dados &#40;tutorial do SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)  
  
##  <a name="bkmk_subscription_requirements"></a>Requisitos de assinatura  
 Antes de criar uma assinatura para um relatório, os seguintes pré-requisitos devem ser cumpridos:  
  
|Requisito|DESCRIÇÃO|  
|-----------------|-----------------|  
|Permissões|Você deve ter acesso ao relatório. Antes de assinar um relatório, você deve ter permissão para exibi-lo.<br /><br /> Sua atribuição de função devem incluir a tarefa “Gerenciar assinaturas individuais”.|  
|Credenciais armazenadas|Para criar uma assinatura, o relatório deve usar credenciais armazenadas ou nenhuma credencial para recuperar dados em tempo de execução. Você não pode assinar um relatório que é configurado para usar as credenciais representadas ou delegadas do usuário atual para conectar-se a uma fonte de dados externa. As credenciais armazenadas podem ser uma conta do Windows ou uma conta de usuário de banco de dados. Para obter mais informações, consulte [especificar credenciais e informações de conexão para fontes de dados de relatório](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)<br /><br /> É necessário ter permissão para exibir o relatório e criar assinaturas individuais. **Eventos agendados e entrega de relatório** devem ser habilitadas no servidor de relatório. Para saber mais, consulte [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../create-manage-subscriptions-native-mode-report-servers.md).|  
|Valores dependentes do usuário em um relatório|Somente para assinaturas padrão, você pode criar assinaturas para relatórios que incorporam informações da conta de usuário em um filtro ou como texto que aparece no relatório. No relatório, o nome da conta de usuário é especificado por uma expressão `User!UserID` resolvida no usuário atual. Ao criar uma assinatura, o usuário que cria a assinatura é considerado o usuário atual.|  
|Nenhuma segurança do item de modelo|Não é possível assinar um relatório do Construtor de Relatórios que use um modelo como uma fonte de dados se o modelo contiver configurações de segurança do item de modelo. Somente relatórios que usam a segurança do item de modelo são incluídos nesta restrição.|  
|Valores de parâmetros|Se o relatório usar parâmetros, um valor de parâmetro deverá ser especificado com o próprio relatório ou na assinatura definida. Se valores padrão forem definidos no relatório, você poderá definir o valor de parâmetro a ser usado como o padrão.|  
  
##  <a name="bkmk_delivery_extensions"></a>Extensões de entrega  
 As assinaturas são processadas no servidor de relatórios e são distribuídas através de extensões de entrega implantadas no servidor. Por padrão, é possível criar assinaturas que enviam relatórios para uma pasta compartilhada ou um endereço de email. Se o servidor de relatório for configurado para o modo integrado do SharePoint, também será possível enviar um relatório para uma biblioteca do SharePoint.  
  
 Quando cria uma assinatura, o usuário pode escolher uma das extensões de entrega disponíveis para determinar como o relatório será entregue. 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui as seguintes extensões de entrega.  
  
|Extensão de entrega|DESCRIÇÃO|  
|------------------------|-----------------|  
|Compartilhamento de Arquivos do Windows|Entrega um relatório como um arquivo de aplicativo estático para uma pasta compartilhada que pode ser acessada na rede.|  
|Email|Entrega uma notificação ou um relatório como um anexo de email ou link de URL.|  
|Biblioteca do SharePoint|Entrega um relatório como um arquivo de aplicativo estático para uma biblioteca do SharePoint que pode ser acessada a partir de um site do SharePoint. O site deve estar integrado a um servidor de relatório executado no modo integrado do SharePoint.|  
|Nulo|O provedor de entrega nulo é uma extensão de entrega altamente especializada usada para pré-carregar um cache com relatórios com parâmetros e prontos para exibição. Esse método não está disponível para usuário em assinaturas individuais. Entrega nula é usada por administradores em assinaturas controladas por dados para melhorar o desempenho do servidor de relatórios através do pré-carregamento do cache.|  
  
> [!NOTE]  
>  Entrega de relatório é uma parte extensível da arquitetura do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Fornecedores de terceiros podem criar extensões de entrega personalizadas para rotear relatórios a locais ou dispositivos diferentes. Para obter mais informações sobre extensões de entrega personalizadas, consulte [Implementing a Delivery Extension](../extensions/delivery-extension/implementing-a-delivery-extension.md).  
  
##  <a name="bkmk_parts_of_subscription"></a>Partes de uma assinatura  
 Uma definição de assinatura consiste nas seguintes partes:  
  
-   Um ponteiro para um relatório que pode ser executado de modo autônomo (isto é, um relatório que usa credenciais armazenadas ou nenhuma credencial).  
  
-   Um método de entrega (por exemplo, email) e configurações para o modo de entrega (como um endereço de email).  
  
-   Uma extensão de renderização para apresentar o relatório em um formato específico.  
  
-   Condições para processar a assinatura, que são expressas como um evento.  
  
     Normalmente, as condições para executar um relatório baseiam-se na hora. Por exemplo, você executar um relatório específico todas as terças-feiras às 15h00 UTC. No entanto, se o relatório for executado como um instantâneo, você pode especificar que a assinatura seja executada sempre que o instantâneo for atualizado.  
  
-   Parâmetros usados ao executar o relatório.  
  
     Os parâmetros são opcionais e especificados somente para relatórios que aceitam valores de parâmetro. Como uma assinatura normalmente é de propriedade do usuário, os valores de parâmetro especificados variam conforme a assinatura. Por exemplo, gerentes de vendas de divisões diferentes usarão parâmetros que retornam dados para sua divisão. Todos os parâmetros devem ter um valor explicitamente definido ou um valor padrão válido.  
  
 As informações de assinatura são armazenadas com relatórios individuais em um banco de dados do servidor de relatório. Você não pode gerenciar assinaturas separadamente do relatório com o qual estão associadas. Observe que as assinaturas não podem ser estendidas para incluir descrições, outros textos personalizados ou outros elementos. As assinaturas podem conter somente os itens listados anteriormente.  
  
##  <a name="bkmk_subscription_processing"></a>Como as assinaturas são processadas  
 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui um processador de agendamento e entrega, que fornece funcionalidade para o agendamento de relatórios e suas entregas aos usuários. O servidor de relatório responde a eventos monitorados continuamente. Quando o evento que corresponde às condições definidas para uma assinatura ocorre, o servidor de relatório lê a assinatura para determinar como processar e entregar o relatório. O servidor de relatório solicita a extensão de entrega que é especificada na assinatura. Após a execução da extensão de entrega, o servidor de relatório extrai informações de entrega da assinatura e as transmite à extensão de entrega para processamento.  
  
 A extensão de entrega renderiza o relatório no formato definido na assinatura e, em seguida, entrega o relatório ou a notificação ao destino especificado. Se não for possível entregar um relatório, uma entrada será registrada no arquivo de log do servidor de relatório. Se desejar oferecer suporte para operações de repetição, configure o servidor de relatório para tentar entregar novamente caso a primeira tentativa falhe.  
  
### <a name="processing-a-standard-subscription"></a>Processando uma assinatura padrão  
 As assinaturas padrão produzem uma instância de um relatório. O relatório é entregue em uma única pasta compartilhada ou nos endereços de email especificados na assinatura. O layout e os dados do relatório não variam. Se o relatório usar parâmetros, uma assinatura padrão será processada com um único valor para cada parâmetro do relatório.  
  
### <a name="processing-a-data-driven-subscription"></a>Processando uma assinatura controlada por dados  
 As assinaturas controladas por dados podem produzir muitas instâncias de relatório que são entregues a vários destinos. O layout do relatório não varia, mas os dados podem variar se os valores de parâmetro forem transmitidos a partir de um conjunto de resultados de assinante. As opções de entrega que afetam a renderização do relatório e a anexação ou o vínculo do relatório ao email também podem variar dependendo do assinante quando os valores são transmitidos a partir do conjunto de linhas.  
  
 As assinaturas controladas por dados podem produzir um grande número de entregas. O servidor de relatório cria um envio para cada linha do conjunto que é retornado da consulta de assinatura.  
  
### <a name="report-delivery-characteristics"></a>Características de entrega de relatório  
 Os relatórios que são entregues por meio de assinaturas padrão normalmente são renderizados como relatórios estáticos. Esses relatórios são baseados no instantâneo de execução de relatório mais recente ou são gerados como um relatório estático para concluir uma entrega. Se a opção **Incluir Link** for selecionada em uma assinatura para um relatório executado sob demanda, o servidor de relatório executará o relatório quando você clicar no hiperlink.  
  
> [!NOTE]  
>  Os relatórios que são entregues por uma URL permanecem conectados ao servidor de relatório e podem ser atualizados ou excluídos entre as exibições. As opções de entrega escolhidas para a assinatura determinam se o relatório será entregue como uma URL, inserido no corpo de uma mensagem de email ou enviado como anexo.  
  
 Os relatórios que são entregues por uma assinatura controlada por dados podem ser gerados novamente enquanto a assinatura está sendo processada. O servidor de relatório não observa uma instância específica de um relatório ou seu conjunto de dados para concluir uma assinatura controlada por dados. Se a assinatura usar valores de parâmetro diferentes para assinantes diferentes, o servidor de relatório gerará o relatório novamente para produzir o resultado necessário. Se os dados subjacentes forem atualizados após a primeira cópia do relatório ser criada e entregue, os usuários que obtiverem relatórios posteriormente no processo poderão ver dados baseados em um conjunto de dados diferente. Você pode usar o relatório executado como um instantâneo para verificar se a mesma instância do relatório é entregue a todos os assinantes. No entanto, se uma atualização agendada do instantâneo ocorrer durante o processamento da assinatura, os usuários ainda poderão obter dados diferentes em seus relatórios.  
  
### <a name="triggering-subscription-processing"></a>Acionando o processamento de assinaturas  
 O servidor de relatório usa dois tipos de eventos para acionar o processamento de assinaturas: um evento controlado por tempo que é especificado em uma agenda ou um evento de atualização de instantâneo.  
  
 Um gatilho controlado por tempo usa uma agenda específica do relatório ou uma agenda compartilhada para especificar quando uma assinatura deve ser executada. Para relatórios sob demanda e em cache, as agendas são a única opção de gatilho.  
  
 Um evento de atualização de instantâneo usa a atualização agendada de um instantâneo de relatório para acionar uma assinatura. Você pode definir uma assinatura que é acionada sempre que o relatório é atualizado com novos dados, com base nas propriedades de execução definidas no relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma assinatura controlada por dados &#40;tutorial do SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Agendamento](schedules.md)   
 [Reporting Services servidor de relatório &#40;modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [Criar e gerenciar assinaturas de servidores de relatório no modo nativo](../create-manage-subscriptions-native-mode-report-servers.md)   
 [Monitorar assinaturas do Reporting Services](monitor-reporting-services-subscriptions.md)  
  
  
