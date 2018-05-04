---
title: Criar e configurar o aplicativo de serviço do Power Pivot na autoridade de certificação | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5748a659aad37878869135c6a3d8358880979fe7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-configure-power-pivot-service-application-in-ca"></a>Criar e configurar o aplicativo de serviço do Power Pivot na autoridade de certificação
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é uma instância de serviço compartilhado do Serviço do Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Cada aplicativo de serviço tem sua própria identidade, definições de configuração, propriedades e armazenamento de dados interno.  
  
 Este tópico contém as seguintes seções:  
  
 [Determinar se deseja criar um novo aplicativo de serviço do Power Pivot](#determine)  
  
 [Criar um aplicativo de serviço do Power Pivot](#CreateApp)  
  
 [Configurar o aplicativo de serviço do Power Pivot](#ConfigApp)  
  
 [Atribuir um aplicativo de serviço do Power Pivot a um aplicativo Web](#AssignGSA)  
  
 [Editar propriedades de aplicativo de serviço](#EditGSA)  
  
##  <a name="determine"></a> Determinar se deseja criar um novo aplicativo de serviço do Power Pivot  
 Uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint deve ter pelo menos um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Um aplicativo de serviço é criado automaticamente se você usar a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para configurar o servidor. Caso contrário, você terá que criar um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] manualmente na Administração Central.  
  
 Criar um aplicativo de serviço torna o serviço disponível e gera o banco de dados de aplicativo de serviço. Dependendo das opções selecionadas ao criar o aplicativo de serviço, uma conexão de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é acrescentada ao grupo de conexão de serviço padrão. Todos os aplicativos Web do SharePoint que assinam o grupo de conexão de serviço padrão obterão acesso imediato ao aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] automaticamente.  
  
 Você pode criar vários aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Embora um aplicativo de serviço seja suficiente para a maioria dos cenários de implantação, você pode criar um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] adicional se seus requisitos de negócio incluírem o seguinte:  
  
-   O uso de uma conta de atualização de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] autônoma para cada aplicativo.  
  
-   O uso de tempos limite diferentes, de histórico do uso e de limites para relatórios de resposta de consulta.  
  
-   A delegação da administração de serviço para uma pessoa diferente. Um administrador verá o histórico da atualização de dados, os dados de uso e outras propriedades apenas para o aplicativo que está administrando. Se você precisar isolar aplicativos Web do SharePoint (por exemplo, se a empresa for um serviço de hospedagem que precisa garantir o isolamento dos dados para os aplicativos Web do SharePoint que pertencem a clientes diferentes), a criação de aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] diferentes pode ajudar a atender aos requisitos de isolamento, garantindo que cada administrador de serviços veja apenas as definições de configuração e as propriedades do aplicativo que gerencia.  
  
 A criação de um aplicativo de serviço adicional introduz novos requisitos para o gerenciamento de associações de serviço. Mais especificamente, ela exigirá que você crie e use listas de associações de serviços personalizadas para cada aplicativo de serviço adicional criado.  
  
 Se você não tiver uma razão específica para criar aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] adicional, use um único aplicativo de serviço para todos os aplicativos Web no farm.  
  
##  <a name="CreateApp"></a> Criar um aplicativo de serviço do Power Pivot  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Na faixa de opções **Aplicativos de Serviço** , clique em **Novo**.  
  
3.  Selecione **Aplicativo de Serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do SQL Server**. Se não aparecer na lista, significa que o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint não está instalado ou configurado corretamente.  
  
4.  Na página **Criar Novo Aplicativo de Serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**, insira um nome para o aplicativo. O padrão é PowerPivotServiceApplication\<número >. Se você estiver criando vários aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , um nome descritivo ajudará outros administradores a entender como o aplicativo é usado.  
  
5.  Em Pool de Aplicativos, crie um novo pool de aplicativos para o aplicativo (recomendável). Selecione ou crie uma conta gerenciada para o pool de aplicativos. Não se esqueça de especificar uma conta de usuário do domínio. Uma conta de usuário de domínio habilita o uso do recurso de conta gerenciado do SharePoint que o deixa atualizar senhas e informações de conta em um único local. Contas de domínio também serão obrigatórias se você pretender diminuir a implantação para incluir instâncias de serviço adicionais a serem executadas sob a mesma identidade.  
  
6.  Em **Servidor de Banco de Dados**, o valor padrão é a instância de Mecanismo de Banco de Dados do SQL Server que hospeda os bancos de dados de configuração de farm. Você pode usar este servidor ou pode escolher um SQL Server diferente.  
  
7.  Em **nome do banco de dados**, o valor padrão é PowerPivotServiceApplication1_\<guid >. Você deve criar um banco de dados exclusivo para cada aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O nome do banco de dados padrão corresponde ao nome padrão do aplicativo de serviço. Se você inseriu um nome de aplicativo de serviço exclusivo, siga uma convenção de nomenclatura semelhante para seu nome de banco de dados de forma que você possa gerenciá-los em conjunto.  
  
8.  Em **Autenticação de Banco de dados**, o padrão é Autenticação do Windows. Se você escolher **Autenticação SQL**, consulte o guia de práticas recomendadas do administrador do SharePoint para saber como usar esse tipo de autenticação em uma implantação do SharePoint.  
  
9. Como opção, marque a caixa de seleção **Adicionar o proxy para este aplicativo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Service ao grupo de proxy padrão do farm.** . Esse procedimento adiciona a conexão de aplicativo de serviço ao grupo de conexões de serviço padrão.  
  
     Você deverá marcar essa caixa de seleção se estiver criando o primeiro aplicativo do serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Deve haver apenas um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no grupo de conexões padrão para garantir o funcionamento correto do Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
     Não adicione o aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ao grupo de conexões padrão se já houver um. A adição de várias entradas do mesmo tipo de aplicativo do serviço não é uma configuração compatível e pode causar erros. Se você estiver criando aplicativos de serviço adicionais, deixe-os fora do grupo de conexões padrão e adicione-os às listas personalizadas.  
  
     Para obter mais informações sobre associações de serviço, consulte [Conectar um aplicativo de serviço do Power Pivot a um aplicativo Web do SharePoint na Administração Central](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
10. Clique em **OK.** O serviço aparecerá ao lado de outros serviços gerenciados na lista de aplicativos de serviço do farm.  
  
##  <a name="ConfigApp"></a> Configurar o aplicativo de serviço do Power Pivot  
 Um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é criado usando uma configuração padrão. As configurações padrão são recomendadas para a maioria dos cenários. Somente as altere se você encontrar um tempo de resposta lento ou conexões removidas, ou se você estiver variando a configuração de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para aplicativos Web do SharePoint específicos.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
     Na lista de aplicativos de serviço, deve aparecer o aplicativo de serviço recém-criado e nomeado. O padrão é **PowerPivotServiceApplication1**.  
  
2.  Clique no aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Isso abre o Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
3.  Na lista **Ações** , no canto superior direito do painel, clique em **Definir configurações do aplicativo de serviço**.  
  
4.  Em **Tempo Limite de Carregamento do Banco de Dados**, aumente ou diminua o valor a ser alterado para definir a espera do serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] por uma resposta da instância do SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) para a qual ele encaminhou uma solicitação de dados de carregamento. Como conjuntos de dados muito grandes levam muito tempo para serem transferidos eletronicamente, você deve aguardar um tempo suficiente para que a instância de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] recupere a pasta de trabalho do Excel e mova os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para uma instância do Analysis Services para processamento da consulta. Como os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] podem ser extraordinariamente grandes, o valor padrão é 30 minutos.  
  
5.  Em **Tempo Limite do Pool de Conexão**, aumente ou diminua o valor para alterar por quantos minutos uma conexão de dados permanecerá aberta. O valor padrão é de 30 minutos. Durante esse período, o serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] reutilizará uma conexão de dados ociosa para solicitações de somente leitura do mesmo usuário do SharePoint para os mesmos dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se nenhuma solicitação adicional for recebida para obter esses dados durante o período especificado, a conexão será removida do pool. Os valores válidos são de 1 a 3.600 segundos. Para obter mais informações sobre pools de conexão, consulte [Referência de definição de configuração &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md).  
  
6.  Em **Tamanho Máximo do Pool de Conexão do Usuário**, aumente ou diminua o valor para alterar o número máximo de conexões ociosas que o serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] criará em pools de conexões individuais para cada usuário do SharePoint, conjunto de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e combinações de versões.  
  
     O valor padrão é de 1000 conexões ociosas. Os valores válidos são -1 (ilimitado), 0 (desabilita pool de conexões do usuário) ou de 1 a 10000.  
  
     Esses pools de conexões permitem que o serviço dê suporte mais eficiente a conexões contínuas para os mesmos dados somente leitura pelo mesmo usuário. Se você desabilitar o pooling de conexão, todas as conexões serão recriadas.  
  
     Observe que a alteração do limite no tamanho do pool de conexões, inclusive a definição como 0, não resultará em conexões removidas. Há pools de conexões para reduzir tempos de espera durante a conexão com os dados. O serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nunca negará uma conexão com base nas configurações do pool de conexões.  
  
7.  Em **Tamanho Máximo do Pool de Conexão Administrativa**, aumente ou diminua o valor para alterar o número de conexões abertas em um pool de conexões criado para uma conexão do serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ao Analysis Services. Cada instância de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] abre uma conexão administrativa separada para a instância do Analysis Services no mesmo computador. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cria um pool separado para reutilizar conexões administrativas com a finalidade de verificar conexões ociosas e monitorar a integridade do servidor. O valor padrão é de 200 conexões. Os valores válidos são -1 (ilimitado), 0 (desabilita pool de conexões administrativas) ou 1 a 10000. Se você selecionar 0, todas as conexões serão recriadas.  
  
8.  Em **Método de Alocação**, é possível especificar o esquema de balanceamento de carga que o Serviço do Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usa para selecionar um aplicativo do serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] específico para o balanceamento de carga de uma solicitação inicial. O padrão é **Baseado na Integridade**, que aloca solicitações com base no estado do servidor, conforme avaliado pela memória disponível e pela utilização do processador. Outra opção é escolher **Rodízio** para alocar solicitações para servidores na mesma ordem de repetição, independentemente de um servidor estar ocupado ou ocioso.  
  
9. Em Atualização de Dados, em **Horário Comercial**, você pode especificar um intervalo de horas que define um dia comercial. Os agendamentos de atualização de dados podem ser realizados depois do fim de um dia útil para escolher dados transacionais que foram gerados durante o horário comercial normal.  
  
10. Em **Conta Autônoma de Atualização de Dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**, você pode especificar um aplicativo destino do Serviço de Repositório Seguro predefinido que armazena uma conta predefinida para executar trabalhos de atualização de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Especifique o nome do aplicativo de destino, e não a ID. O aplicativo de destino para atualização de dados autônoma será criado automaticamente se você usar a opção Novo Servidor na Instalação do SQL Server para instalar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Caso contrário, crie o aplicativo de destino manualmente. Para obter instruções sobre como configurar a conta, consulte [Configurar a conta autônoma de atualização de dados do Power Pivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493).  
  
11. Em **Permitir que os usuários insiram credenciais personalizadas do Windows**, é possível marcar ou desmarcar a caixa de seleção para especificar se os proprietários da agenda podem inserir credenciais do Windows arbitrárias para executar uma agenda de atualização de dados. Se você marcar essa caixa de seleção, o aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] criará e gerenciará um aplicativo de destino para cada conjunto de credenciais armazenadas. Para obter mais informações, consulte [Configurar credenciais armazenadas para atualização de dados do Power Pivot (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75).  
  
12. Em **Tamanho Máximo do Histórico de Processamento**, você pode especificar por quanto tempo deseja reter um registro histórico de processamento de atualização de dados. Essas informações aparecem nas páginas do histórico de atualização de dados mantidas para cada pasta de trabalho que usa atualização de dados. Elas também são exibidas no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
13. Em Coleção de Dados de Uso, em **Intervalo de Relatório de Consulta**, especifique um intervalo para informar estatísticas de consulta. Estatísticas de consulta são relatadas como um único evento para minimizar a comunicação servidor a servidor.  
  
14. Em Histórico de Dados de Uso, especifique por quanto tempo você deseja manter um registro histórico de dados de uso. As informações de uso são exibidas no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Os relatórios serão menos eficazes se você especificar um valor muito baixo para o histórico de dados de uso.  
  
15. Em Coleção de Dados de Uso, em cada limite de resposta de consulta, especifique um limite superior que determina onde uma categoria para e outra começa. Estas categorias estabelecem uma linha de base em relação à qual o comportamento de consulta é medido. Você pode usar essas categorias para monitorar tendências de tempos de resposta de consulta para seu sistema. Essas informações são exibidas no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
16. Clique em **OK** para salvar as alterações.  
  
     Alterações do tempo limite de carregamento ou do método de alocação somente são aplicadas a novas solicitações de entrada. Solicitações em andamento estão sujeitas aos valores que estavam em vigor quando a solicitação foi recebida.  
  
##  <a name="AssignGSA"></a> Atribuir um aplicativo de serviço do Power Pivot a um aplicativo Web  
 Depois de configurar um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , você pode atribuí-lo a um aplicativo Web acrescentando-o à lista de conexão de aplicativo de serviço para aquele aplicativo Web. Isso pode ser feito de duas maneiras:  
  
-   Acrescente-o ao grupo de conexão **Padrão** . O *grupo de conexão padrão* é uma coleção de conexões de aplicativo de serviço que estão disponíveis para qualquer aplicativo Web que faça referência a ele. Você deve adicionar um aplicativo do serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a essa lista.  
  
-   Crie uma lista de conexão **Personalizada** para um aplicativo Web específico. Se você criou vários aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , poderá escolher qual deseja usar selecionando-o em uma lista personalizada.  
  
 O grupo de conexões padrão aceitará mais de um aplicativo de serviço do mesmo tipo. No entanto, saiba que a adição de mais de um aplicativo do serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a essa lista não é uma configuração compatível.  
  
1.  Na Administração Central, em **Gerenciamento de Aplicativo**, clique em **Gerenciar aplicativos Web**.  
  
2.  Selecione o aplicativo para o qual deseja atribuir uma conexão (por exemplo, SharePoint -80).  
  
3.  Clique em **Conexões de Serviço**.  
  
4.  Em **Editar o seguinte grupo de associações**, selecione **padrão** ou **[personalizado]**.  
  
5.  Para **[personalizado]**, marque a caixa de seleção ao lado de cada conexão de aplicativo de serviço a ser usada. Se você tiver vários aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (indicado por Tipo definido como **Proxy de Aplicativo de Serviço Power Pivot**), escolha apenas um.  
  
6.  Clique em **OK**.  
  
##  <a name="EditGSA"></a> Editar propriedades de aplicativo de serviço  
 Use as instruções seguintes para reabrir a página de propriedades que especifica o nome de aplicativo de serviço, o pool de aplicativos, as configurações de banco de dados e as associações de serviço.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Selecione, mas não clique, o aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Você pode clicar no nome do tipo para selecionar uma linha inteira.  
  
3.  Clique em **Propriedades** na faixa de opções.  
  
## <a name="see-also"></a>Consulte também  
 [Administração e configuração de servidor do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
