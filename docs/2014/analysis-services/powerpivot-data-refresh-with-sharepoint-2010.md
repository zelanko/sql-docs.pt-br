---
title: Atualização de dados do PowerPivot com SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 01b54e6f-66e5-485c-acaa-3f9aa53119c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1af27b0571ef073a5ada2937b93b6cc0487974d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143737"
---
# <a name="powerpivot-data-refresh-with-sharepoint-2010"></a>Atualização de dados PowerPivot com SharePoint 2010
  A atualização de dados [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] é uma operação agendada no servidor que consulta fontes de dados externas para atualizar dados [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] inseridos em uma pasta de trabalho do Excel 2010 que é armazenada em uma biblioteca de conteúdo.  
  
 A atualização de dados é um recurso interno do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint, mas usá-lo exige que você execute serviços específicos e trabalhos de timer no farm do SharePoint 2010. Etapas administrativas adicionais, como a instalação de provedores de dados e a verificação de permissões de banco de dados, costumam ser necessárias para o êxito na atualização de dados.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e serviços do Excel do SharePoint Server 2013 usam uma arquitetura diferente para atualização de dados [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] modelos de dados. A nova arquitetura utiliza os Serviços do Excel como componente primário para carregar modelos de dados PowerPivot. A arquitetura de atualização de dados anterior utilizada baseava-se em um servidor que executava o Serviço do Sistema PowerPivot e o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no modo do SharePoint para carregar modelos de dados. Para obter mais informações, consulte [atualização de dados do PowerPivot com o SharePoint 2013](power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md).  
  
 **Neste tópico:**  
  
 [Etapa 1: Habilitar o serviço de Store seguro e gerar uma chave mestra](#bkmk_services)  
  
 [Etapa 2: Desativar as opções de credenciais que você não deseja dar suporte](#bkmk_creds)  
  
 [Etapa 3: Criar aplicativos de destino para armazenar credenciais usadas na atualização de dados](#bkmk_stored)  
  
 [Etapa 4: Configurar o servidor para atualização de dados evolutiva](#bkmk_scale)  
  
 [Etapa 5: Instalar provedores de dados usados para importar dados do PowerPivot](#bkmk_installdp)  
  
 [Etapa 6: Conceder permissões para criar agendas e acessar fontes de dados externas](#bkmk_accounts)  
  
 [Etapa 7: Habilitar a atualização da pasta de trabalho para atualização de dados](#bkmk_upgradewrkbk)  
  
 [Etapa 8: Verificar a configuração de atualização de dados](#bkmk_verify)  
  
 [Modificar definições de configuração para atualização de dados](#bkmk_config)  
  
 [Reagendar o trabalho de timer de atualização de dados PowerPivot](#configTimerJob)  
  
 [Desabilitar o trabalho de Timer de atualização de dados](#bkmk_disableDR)  
  
 Após a verificação de que o ambiente de servidor e as permissões estão configurados, a atualização de dados estará pronta para uso. Para usar a atualização de dados, um usuário SharePoint cria uma agenda em uma pasta de trabalho PowerPivot que especifica a frequência da atualização de dados. A criação da agenda costuma ser feita pelo proprietário da pasta de trabalho ou pelo autor que publicou o arquivo no SharePoint. Essa pessoa cria e gerencia as agendas de atualização de dados para as pastas de trabalho de sua propriedade. Para obter mais informações, consulte [agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
##  <a name="bkmk_services"></a> Etapa 1: Habilitar o serviço de Store seguro e gerar uma chave mestra  
 A atualização de dados PowerPivot depende do Serviço de Repositório Seguro para fornecer as credenciais usadas para executar trabalhos de atualização de dados e conectar-se a fontes de dados externas que usam credenciais armazenadas.  
  
 Se você instalou o PowerPivot para SharePoint usando a opção Novo Servidor, o Serviço de Repositório Seguro foi configurado para você. Para outros cenários de instalação, crie e configure um aplicativo de serviço e gere uma chave de criptografia mestra para o Serviço de Repositório Seguro.  
  
> [!NOTE]  
>  Você deve ser um administrador de farm para configurar o Serviço de Repositório Seguro ou delegar a administração do Serviço de Repositório Seguro a outro usuário. Você precisa ser um administrador de aplicativo de serviço para definir ou modificar configurações habilitadas.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Na faixa de opções Aplicativos de Serviço, em Criar, clique em **Novo**.  
  
3.  Selecione **Serviço de Repositório Seguro**.  
  
4.  Na página **Criar Aplicativo de Repositório Seguro** , insira um nome para o aplicativo.  
  
5.  Em **Banco de Dados**, especifique a instância do SQL Server que hospedará o banco de dados para este aplicativo de serviço. O valor padrão é a instância de Mecanismo de Banco de Dados do SQL Server que hospeda os bancos de dados de configuração de farm.  
  
6.  Em **Nome do Banco de Dados**, insira o nome do banco de dados de aplicativo de serviço. O valor padrão é Secure_Store_Service_DB_\<guid >. O nome padrão corresponde ao nome padrão do aplicativo de serviço. Se você inseriu um nome de aplicativo de serviço exclusivo, siga uma convenção de nomenclatura semelhante para seu nome de banco de dados de forma que você possa gerenciá-los em conjunto.  
  
7.  Em **Autenticação de Banco de dados**, o padrão é Autenticação do Windows. Se você escolher Autenticação SQL, consulte o guia do administrador do SharePoint para saber como usar o tipo de autenticação no farm.  
  
8.  No Pool de Aplicativos, selecione **Criar novo pool de aplicativos** . Especifique um nome descritivo que ajudará outros administradores do servidor a identificar como o pool de aplicativos é usado.  
  
9. Selecione uma conta de segurança para o pool de aplicativos. Especifique uma conta gerenciada para usar uma conta de usuário de domínio.  
  
10. Aceite os valores padrão restantes e clique em **OK.** O aplicativo de serviço aparecerá ao lado de outros serviços gerenciados na lista de aplicativos de serviço do farm.  
  
11. Clique no aplicativo de Serviço de Repositório Seguro na lista.  
  
12. Na faixa de opções Aplicativos de Serviço, clique em **Gerenciar**.  
  
13. Em Gerenciamento de Chaves, clique em **Gerar Nova Chave**.  
  
14. Digite e confirme uma frase secreta. A frase de senha será usada para adicionar aplicativos de serviço compartilhado do repositório seguro.  
  
15. Clique em **OK**.  
  
 O log de auditoria das operações do Serviço de Repositório, que é útil para a solução de problemas, deve ser habilitado antes de estar disponível. Para obter mais informações sobre como habilitar o log, consulte [Configurar o Serviço de Repositório Seguro (SharePoint 2010)](http://go.microsoft.com/fwlink/p/?LinkID=223294).  
  
##  <a name="bkmk_creds"></a> Etapa 2: Desativar as opções de credenciais que você não deseja dar suporte  
 A atualização de dados PowerPivot fornece três opções de credenciais em uma agenda de atualização de dados. Quando o proprietário de uma pasta de trabalho agenda a atualização de dados, ele escolhe uma dessas opções, determinando, assim, a conta em que o trabalho de atualização de dados será executado. Como administrador, você pode determinar que opções de credenciais estão disponíveis para proprietários de agendas.  
  
 Você deve ter no mínimo uma opção disponível para que a atualização de dados funcione.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 A opção 1, **Usar a conta de atualização de dados configurada pelo administrador**, sempre aparece na página de definição de agenda, mas funciona somente se você configurar a conta de atualização de dados autônoma. Para obter mais informações sobre como criar a conta, consulte [configurar a conta autônoma PowerPivot Data Refresh &#40;PowerPivot para SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
 A opção 2, **Conectar usando as seguintes credenciais de usuário do Windows**, sempre aparece na página, mas só funciona quando você habilita a opção **Permitir que os usuários insiram credenciais personalizadas do Windows** na página de configuração de aplicativos de serviço. Essa opção é habilitada por padrão, mas você pode desabilitá-la se as desvantagens de usá-la superarem as vantagens (veja abaixo).  
  
 A opção 3, **Conecte-se usando as credenciais salvas no SSS**, sempre aparece na página, mas funciona somente quando o proprietário de uma agenda fornece um aplicativo de destino válido. Um administrador deve criar esses aplicativos de destino antecipadamente e fornecer o nome do aplicativo para aqueles que criarem agendas de atualização de dados. Para obter mais informações sobre como criar um aplicativo de destino para dados de operações de atualização, consulte [configurar credenciais armazenadas para atualização de dados do PowerPivot do &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
 **Configurando a opção de credencial 2, "Conectar-se usando as seguintes credenciais de usuário do Windows"**  
  
 Um aplicativo de serviço PowerPivot inclui uma opção de credencial que permite a proprietários de agendas especificar um nome de usuário e senha arbitrários do Windows para executar um trabalho de atualização de dados. Esta é a segunda opção de credencial na página de definição de agenda:  
  
 ![SSAS_PPS_ScheduleDataRefreshCreds](media/ssas-pps-scheduledatarefreshcreds.gif "SSAS_PPS_ScheduleDataRefreshCreds")  
  
 Esta opção de credencial está habilitada por padrão. Quando essa opção de credencial está habilitada, o Serviço do Sistema PowerPivot gera um aplicativo de destino no Serviço de Repositório Seguro para armazenar o nome de usuário e a senha especificados pelo proprietário da agenda. Um aplicativo de destino gerado é criado usando essa convenção de nomenclatura: PowerPivotDataRefresh_\<guid >. Um aplicativo de destino é criado para cada conjunto de credenciais do Windows. Se já houver um aplicativo de destino pertencente ao Serviço do Sistema PowerPivot e ele armazenar o nome de usuário e a senha especificados pela pessoa que definiu a agenda, o Serviço do Sistema PowerPivot usará o aplicativo de destino em vez de criar um novo.  
  
 A principal vantagem de usar essa opção de credencial é a facilidade de uso e simplicidade. O trabalho antecipado é mínimo porque os aplicativos de destino são criados por você. Além disso, a execução da atualização de dados com as credenciais do proprietário da agenda (que muito provavelmente é a pessoa que criou a pasta de trabalho) simplifica o downstream dos requisitos de permissão. Muito provavelmente, esse usuário já tem permissões no banco de dados de destino. Quando a atualização de dados é executada com a identidade de usuário do Windows dessa pessoa, qualquer conexão de dados que especificar ‘usuário atual’ funcionará automaticamente.  
  
 A desvantagem é a capacidade limitada de gerenciamento. Embora os aplicativos de destino sejam criados automaticamente, eles não são excluídos automaticamente nem atualizados conforme a mudança das informações de conta. As políticas de expiração de senha podem fazer com que esses aplicativos de destino se tornem desatualizados. Os trabalhos de atualização de dados que usam credenciais expiradas começarão a falhar. Quando isso ocorrer, os proprietários da agenda deverão atualizar suas credenciais fornecendo os valores atuais de nome de usuário e senha em uma agenda de atualização de dados. Um novo aplicativo de destino será criado nesse momento. Com o passar do tempo, conforme os usuários adicionarem e revisarem as informações de credenciais em suas agendas de atualização de dados, você poderá achar que tem um grande número de aplicativos de destino gerados automaticamente em seu sistema.  
  
 No momento, não há como determinar qual desses aplicativos de destino estão ativos ou inativos, nem há como rastrear um aplicativo de destino específico para as agendas de atualização de dados que o usam. Em geral, você deve deixar os aplicativos de destino de lado, pois excluí-los pode corromper as agendas de atualização de dados existentes. Excluir um aplicativo de destino que ainda está em uso faz com que a atualização de dados falhe exibindo a mensagem “Aplicativo de destino não encontrado” na página do histórico de atualização de dados da pasta de trabalho.  
  
 Se você optar por desabilitar essa opção de credencial, poderá excluir com segurança todos os aplicativos de destino gerados para a atualização de dados PowerPivot.  
  
 **Desabilitando o uso de credenciais arbitrárias do Windows em agendas de atualização de dados**  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar Aplicativos de Serviço**.  
  
2.  Clique no nome do aplicativo de serviço PowerPivot. O Painel de Gerenciamento do PowerPivot é exibido.  
  
3.  Em Ações, clique em **Configurar parâmetros do aplicativo de serviço** para abrir a página Configurações do Aplicativo de Serviço PowerPivot.  
  
4.  Na seção Atualização de Dados, desmarque a caixa de seleção **Permitir que os usuários insiram credenciais personalizadas do Windows** .  
  
     ![SSAS_PowerPivotDatarefreshOptions_AllowUser](media/ssas-powerpivotdatarefreshoptions-allowuser.gif "SSAS_PowerPivotDatarefreshOptions_AllowUser")  
  
##  <a name="bkmk_stored"></a> Etapa 3: Criar aplicativos de destino para armazenar credenciais usadas na atualização de dados  
 Depois da configuração do Serviço de Repositório Seguro, os administradores do SharePoint podem criar aplicativos de destino para disponibilizar as credenciais armazenadas para fins de atualização de dados, inclusive a conta de atualização de dados autônoma do PowerPivot ou qualquer outra conta usada para executar o trabalho ou para conectar-se a fontes de dados externas.  
  
 Conforme dito na seção anterior, é necessário criar aplicativos de destino para poder usar certas opções de credenciais. Especificamente, é necessário criar aplicativos de destino para a conta de atualização de dados autônoma do PowerPivot, além de credenciais armazenadas adicionais que se espera usar em operações de atualização de dados.  
  
 Para obter mais informações sobre como criar aplicativos de destino que contêm credenciais armazenadas, consulte [configurar a conta autônoma PowerPivot Data Refresh &#40;PowerPivot para SharePoint&#41; ](configure-unattended-data-refresh-account-powerpivot-sharepoint.md) e [ Configurar credenciais armazenadas para atualização de dados do PowerPivot do &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
##  <a name="bkmk_scale"></a> Etapa 4: Configurar o servidor para atualização de dados evolutiva  
 Por padrão, cada instalação do PowerPivot para SharePoint oferece suporte a consultas sob demanda e atualizações de dados agendadas.  
  
 Para cada instalação, é possível especificar se a instância de servidor do Analysis Services oferece suporte a consultas e atualizações de dados agendadas, ou se é dedicada a um tipo de operação específico. Se houver várias instalações do PowerPivot para SharePoint em seu farm, você poderá tornar um servidor dedicado apenas às operações de atualização de dados se achar que os trabalhos estão atrasados ou falhando.  
  
 Além disso, se o hardware subjacente permitir, é possível aumentar o número de trabalhos de atualização de dados que podem ser executados em paralelo. Por padrão, o número de trabalhos que podem ser executados em paralelo é calculado com base na memória do sistema, mas você pode aumentar esse número se tiver capacidade de CPU adicional para suportar a carga de trabalho.  
  
 Para obter mais informações, consulte [configurar dedicado de atualização de dados ou processamento Query-Only &#40;PowerPivot para SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md).  
  
##  <a name="bkmk_installdp"></a> Etapa 5: Instalar provedores de dados usados para importar dados do PowerPivot  
 Uma operação de atualização de dados é essencialmente uma repetição de uma operação de importação que recuperou os dados originais. Isso significa que os mesmos provedores de dados usados para importar os dados no aplicativo cliente PowerPivot também devem ser instalados no servidor PowerPivot.  
  
 Você deve ser um administrador local para instalar provedores de dados em um servidor do Windows. Se você for instalar drivers adicionais, instale-os em cada computador do farm do SharePoint que tem uma instalação do PowerPivot para SharePoint. Se você tiver vários servidores PowerPivot no farm, deverá instalar os provedores em cada um deles.  
  
 Lembre-se de que os servidores SharePoint são aplicativos de 64 bits. Verifique se instalou a versão de 64 bits dos provedores de dados que você está usando para dar suporte a operações de atualização de dados.  
  
##  <a name="bkmk_accounts"></a> Etapa 6: Conceder permissões para criar agendas e acessar fontes de dados externas  
 Os proprietários ou autores de pastas de trabalho precisam ter permissão **Colaborar** para agendar a atualização de dados em uma pasta de trabalho. Com esse nível de permissão, a pessoa pode abrir e editar a página de configuração de atualização de dados da pasta de trabalho para especificar as credenciais e informações de agendamento usadas para atualizar os dados.  
  
 Além das permissões do SharePoint, as permissões de banco de dados em fontes de dados externas também devem ser revisadas para verificar se as contas usadas durante a atualização de dados têm direitos de acesso suficientes aos dados. Determinar os requisitos de permissão exige uma avaliação cautelosa de sua parte, pois as permissões que você precisa conceder variam de acordo com a cadeia de conexão da pasta de trabalho e a identidade de usuário sob a qual o trabalho de atualização de dados está em execução.  
  
 **Por que as cadeias de caracteres de conexão existentes em uma pasta de trabalho PowerPivot são importantes para operações de atualização de dados do PowerPivot**  
  
 Quando a atualização de dados é executada, o servidor envia uma solicitação de conexão para a fonte de dados externa usando a cadeia de conexão que foi criada quando os dados foram importados inicialmente. O local do servidor, o nome do banco de dados e os parâmetros de autenticação especificados na cadeia de conexão serão reutilizados durante a atualização de dados para acessar as mesmas fontes de dados. A cadeia de conexão e sua construção geral não podem ser modificadas para a atualização de dados. Elas são reutilizadas simplesmente como estão durante a atualização de dados. Em alguns casos, se você usar uma autenticação que não seja do Windows para conectar-se a uma fonte de dados, poderá substituir o nome de usuário e a senha na cadeia de conexão. Mais detalhes sobre isso são fornecidos neste tópico.  
  
 Para a maioria das pastas de trabalho, a opção de autenticação padrão na conexão é usar conexões confiáveis ou a segurança integrada do Windows, resultando em cadeias de conexão que incluem `SSPI=IntegratedSecurity` ou `SSPI=TrustedConnection`. Quando essa cadeia de conexão é usada durante a atualização de dados, a conta usada para executar o trabalho de atualização de dados torna-se o ‘usuário atual’. Como tal, essa conta precisa de permissões de leitura em qualquer fonte de dados externa que seja acessada por uma conexão confiável.  
  
 **Você habilitou o PowerPivot conta de atualização autônoma de dados?**  
  
 Em caso positivo, você deve conceder permissões de leitura a essa conta nas fontes de dados que são acessadas durante a atualização de dados. O motivo pelo qual essa conta precisa de permissões de leitura é porque, em uma pasta de trabalho que usa as opções de autenticação padrão, a conta autônoma será o ‘usuário atual’ durante a atualização de dados. A menos que o proprietário da agenda substitua as credenciais na cadeia de conexão, essa conta precisará de permissões de leitura em qualquer quantidade de fontes de dados que forem ativamente usadas em sua organização.  
  
 **Você está usando a opção de credencial 2: permitir que o proprietário da agenda Insira um nome de usuário do Windows e uma senha?**  
  
 Normalmente, os usuários que criam pastas de trabalho PowerPivot já possuem permissões suficientes porque eles já importaram os dados inicialmente. Se esses usuários configurarem a atualização de dados subsequentemente para ser executada sob sua própria identidade de usuário do Windows, sua conta de usuário do Windows, que já tem direitos no banco de dados, será usada para recuperar dados durante a atualização de dados. As permissões existentes devem ser suficientes.  
  
 **Você está usando a opção de credencial 3: usando um aplicativo de destino do serviço de Store de seguro para fornecer uma identidade de usuário para executar trabalhos de atualização de dados?**  
  
 Qualquer conta usada para executar um trabalho de atualização de dados precisa de permissões de leitura, pelos mesmos motivos descritos para a conta de atualização de dados autônoma do PowerPivot.  
  
 **Como verificar as cadeias de caracteres de conexão para determinar se é possível substituir as credenciais usadas durante a atualização de dados**  
  
 Conforme dito anteriormente, você pode substituir um nome de usuário e uma senha diferentes no nível do trabalho de atualização de dados se a conexão estiver usando uma autenticação que não seja do Windows (por exemplo, autenticação do SQL Server). As credenciais que não são do Windows são transmitidas na cadeia de conexão por meio dos parâmetros de ID de usuário e senha. Se sua pasta de trabalho contiver uma cadeia de conexão com esses parâmetros, você poderá especificar opcionalmente um nome de usuário e uma senha diferentes para atualizar os dados dessa fonte de dados.  
  
 As etapas a seguir explicam como determinar se você tem uma cadeia de conexão que aceita substituições de nomes de usuário e senhas.  
  
1.  Abra a pasta de trabalho no Excel.  
  
2.  Abra a janela do PowerPivot (no Excel, na faixa PowerPivot, clique em Janela do PowerPivot).  
  
3.  Clique em **Design**.  
  
4.  Clique em **Conexões Existentes**.  
  
     Todas as conexões usadas na pasta de trabalho são listadas em **Conexões de Dados PowerPivot**.  
  
5.  Selecione a conexão e clique em **Editar**e em **Avançado**. A cadeia de conexão estará no final da página.  
  
 Se você vir **Integrated Security=SSPI** na cadeia de conexão, não poderá substituir as credenciais nessa cadeia de conexão. A conexão sempre usará o usuário atual. Qualquer credencial fornecida será ignorada.  
  
 Se você vir **Persist Security Info = False, Password =\* \* \* \* \* \* \* \* \* \* \*, UserID =\<userlogin >**, em seguida, você tem uma cadeia de caracteres de conexão que aceita substituições de credenciais. As credenciais que aparecem na cadeia de conexão (como UserID e Password) não são credenciais do Windows, e sim logons de bancos de dados ou outras contas de acesso válidas para a fonte de dados de destino.  
  
 **Como substituir credenciais na cadeia de conexão**  
  
 A substituição de credenciais é feita por meio da especificação das credenciais da fonte de dados na agenda de atualização de dados. Como administrador, você pode fornecer um aplicativo de destino no Serviço de Repositório Seguro que mapeia as credenciais usadas para acessar dados externos. O proprietário da agenda pode inserir a ID do aplicativo de destino na agenda de atualização de dados definida por ele. Para obter mais informações sobre como criar este aplicativo de destino, consulte [configurar credenciais armazenadas para atualização de dados do PowerPivot do &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
 Opcionalmente, o proprietário da agenda pode digitar um conjunto de credenciais que são usadas para conectar-se a fontes de dados durante a atualização de dados. A ilustração a seguir mostra essa opção de fonte de dados na página de definição da agenda.  
  
 ![SSAS_PowerPivotKJ_DataRefreshDSOptions](media/ssas-powerpivotkj-datarefreshdsoptions.gif "SSAS_PowerPivotKJ_DataRefreshDSOptions")  
  
 **Requisitos de acesso de dados de identificação**  
  
 Conforme dito nas seções anteriores, a conta usada para executar a atualização de dados e conectar-se a fontes de dados externas é geralmente a mesma. Sendo assim, a conta usada para acessar fontes de dados externas é determinada pelo conjunto de opções nessa parte da página da agenda de atualização de dados. Ela pode ser a conta de atualização de dados autônoma do PowerPivot, a conta de um usuário individual do Windows ou a conta armazenada em um aplicativo de destino predefinido.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 Em casos em que a conta usada para executar a atualização de dados é diferente da conta usada para importar dados (por exemplo, a conta de atualização de dados autônoma do PowerPivot por meio da opção 1, ou outro conjunto de credenciais armazenadas por meio da opção de credencial 3), você precisará criar um novo logon de banco de dados para essa conta e conceder a ela permissões de leitura nas fontes de dados externas.  
  
 Depois de saber quais contas exigem acesso aos dados, você pode começar a verificar as permissões nas fontes de dados que são mais comumente usadas nas pastas de trabalho PowerPivot. Comece com os data warehouses ou bancos de dados de relatórios que são ativamente usados, mas também peça a opinião dos seus usuários mais ativos do PowerPivot para descobrir que fontes de dados eles estão usando. Se você tiver uma lista de fontes de dados, poderá começar a verificar cada uma delas para confirmar se as permissões estão definidas corretamente.  
  
##  <a name="bkmk_upgradewrkbk"></a> Etapa 7: Habilitar a atualização da pasta de trabalho para atualização de dados  
 Por padrão, pastas de trabalho criadas usando a versão [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] do PowerPivot para Excel não podem ser configuradas para a atualização de dados agendada em uma versão [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] do PowerPivot para SharePoint. Se você hospedar versões mais recentes e anteriores de pastas de trabalho PowerPivot em seu ambiente do SharePoint, deverá primeiro atualizar quaisquer pastas de trabalho [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] antes de agendá-las para atualização de dados automática no servidor.  
  
##  <a name="bkmk_verify"></a> Etapa 8: Verificar a configuração de atualização de dados  
 Para verificar a atualização de dados, você deve ter uma pasta de trabalho PowerPivot publicada em um site do SharePoint. Você deve ter permissões de colaboração na pasta de trabalho e permissões para acessar qualquer fonte de dados incluída na agenda de atualização de dados.  
  
 Quando você criar a agenda, marque a caixa de seleção **Também atualizar o mais rápido possível** para executar a atualização de dados imediatamente. Em seguida, você pode verificar a página do histórico de atualização de dados dessa pasta de trabalho para confirmar se foi executada com êxito. Lembre-se de que o trabalho de timer da Atualização de Dados PowerPivot é executado a cada minuto. Levará no mínimo esse tempo para obter a confirmação de que a atualização de dados foi bem-sucedida.  
  
 Tente todas as opções de credenciais para as quais planeja oferecer suporte. Por exemplo, se você tiver configurado a conta de atualização de dados autônoma do PowerPivot, verifique se a atualização de dados ocorre usando essa opção. Para obter mais informações sobre agendamento e exibindo informações de status, consulte [agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41; ](schedule-a-data-refresh-powerpivot-for-sharepoint.md) e [histórico de atualização de dados de exibição &#40;o PowerPivot para SharePoint &#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
 Se a atualização de dados falhar, consulte a página [Troubleshooting PowerPivot Data Refresh](http://go.microsoft.com/fwlink/?LinkID=223279) no wiki do TechNet para saber quais são as soluções possíveis.  
  
##  <a name="bkmk_config"></a> Modificar definições de configuração para atualização de dados  
 Cada aplicativo de serviço PowerPivot tem parâmetros de configuração que afetam as operações de atualização de dados. Esta seção explica como modificar essas definições.  
  
###  <a name="procIntervals"></a> Defina o 'horário comercial' para determinar fora do horário de processamento  
 Os usuários do SharePoint que agendam operações de atualização de dados podem especificar uma hora de início antes de "Depois do horário comercial". Isso poderá ser útil se eles desejarem recuperar dados de transações comerciais que foram acumulados durante o dia comercial. Como administrador de farm, você pode especificar o intervalo de horas que melhor defina um dia comercial para sua organização. Se você definir o dia comercial como de 4h às 20h, o processamento da atualização de dados baseada em uma hora de início "Depois do horário comercial" iniciará às 20h01.  
  
 Solicitações de atualização de dados executadas fora do horário comercial são adicionadas à fila na ordem de recebimento. Solicitações individuais são processadas conforme os recursos do servidor se tornam disponíveis.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar Aplicativos de Serviço**.  
  
2.  Clique no nome do aplicativo de serviço PowerPivot. O Painel de Gerenciamento do PowerPivot é exibido.  
  
3.  Em Ações, clique em **Configurar parâmetros do aplicativo de serviço** para abrir a página Configurações do Aplicativo de Serviço PowerPivot.  
  
4.  Na seção Atualização de Dados, em Horário comercial, digite uma hora de início e uma hora de término que definam o período de processamento depois do horário comercial.  
  
     Se não desejar definir um período de processamento fora do horário comercial, você poderá digitar o mesmo valor para Hora de Início e Hora de Término (por exemplo, 12h para os dois horários). No entanto, lembre-se de que as páginas de definição da agenda dos sites do SharePoint ainda terão "Depois do horário comercial" como uma opção. Os usuários que selecionarem essa opção em um farm que não tem nenhum intervalo de processamento fora do horário comercial definido, eventualmente, obterão erros de atualização de dados pois os trabalhos de processamento não serão iniciados.  
  
5.  Clique em **OK**.  
  
###  <a name="usagehist"></a> Limitar por quanto tempo o histórico de dados é retido  
 O histórico de atualização de dados é um registro detalhado das mensagens de êxito e de falha geradas por operações de atualização de dados ao longo do tempo. As informações do histórico são coletadas e gerenciadas por meio do sistema de coleta de dados de uso no farm. Dessa forma, limites que você define para o histórico de dados de uso também se aplicam ao histórico de atualização de dados. Como os relatórios de atividade de uso reúnem dados de todo o sistema PowerPivot, uma única configuração de histórico é usada para controlar a retenção de dados de controle para o histórico de atualização de dados e todos os outros dados de uso que são coletados e armazenados.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar Aplicativos de Serviço**.  
  
2.  Clique no nome do aplicativo de serviço PowerPivot. O Painel de Gerenciamento do PowerPivot é exibido.  
  
3.  Em Ações, clique em **Configurar parâmetros do aplicativo de serviço** para abrir a página Configurações do Aplicativo de Serviço PowerPivot.  
  
4.  Na seção Coleta de Dados de Uso, em Histórico de Dados de Uso, digite o número de dias dos quais você deseja manter um registro de atividades de atualização de dados para cada pasta de trabalho.  
  
     O padrão é 365 dias. O valor mínimo é 1 dia e o máximo é 5.000 dias. 0 especifica um período de retenção ilimitado. Os dados nunca são excluídos. Observe que não há configuração para desativar o histórico.  
  
5.  Clique em **OK**.  
  
 As informações do histórico são disponibilizadas para os usuários do SharePoint quando eles escolhem a opção Gerenciar Atualização de Dados em uma pasta de trabalho que tem um histórico de atualização de dados. Essas informações também são usadas no Painel de Gerenciamento PowerPivot utilizado pelos administradores de farm para gerenciar operações do serviço PowerPivot. Para obter mais informações, consulte [histórico de atualização de dados de exibição &#40;PowerPivot para SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
 O armazenamento físico de longo prazo de dados de histórico está no banco de dados do aplicativo do serviço PowerPivot. Para obter mais informações sobre como os dados de uso são coletados e armazenados, consulte [coleta de dados de uso do PowerPivot](power-pivot-sharepoint/power-pivot-usage-data-collection.md).  
  
##  <a name="configTimerJob"></a> Reagendar o trabalho de timer de atualização de dados PowerPivot  
 A atualização de dados agendada é disparada pelo trabalho de timer da Atualização de Dados PowerPivot que examina informações da agenda no banco de dados do aplicativo do serviço PowerPivot em intervalos de um minuto. Quando a atualização de dados está agendada para começar, o trabalho de timer adiciona a solicitação a uma fila de processamento em um servidor PowerPivot disponível.  
  
 Você pode aumentar o período de tempo entre exames como uma técnica de ajuste do desempenho. Você também pode desabilitar o trabalho de timer para interromper temporariamente as operações de atualização de dados ao solucionar problemas.  
  
 A configuração padrão é um minuto que é o valor mais baixo que pode ser especificado. Esse valor é recomendado porque fornece o resultado mais previsível para agendas que executam em horários arbitrários ao longo do dia. Por exemplo, se um usuário agendar a atualização de dados para as 16h15, e o trabalho de timer examinar as agendas a cada minuto, a solicitação de atualização de dados agendada será detectada às 16h15 e o processamento ocorrerá alguns minutos depois das 16h15.  
  
 Se você aumentar o intervalo de exame para que ele seja executado com pouca frequência (por exemplo, uma vez por dia à meia-noite), todas as operações de atualização de dados que foram agendadas para serem executadas nesse intervalo serão adicionadas à fila de processamento ao mesmo tempo, podendo sobrecarregar o servidor e privar outros aplicativos de recursos do sistema. Dependendo do número de atualizações agendadas, a fila de processamento de operações de atualização de dados poderá aumentar de tal forma que nenhum trabalho poderá ser concluído. As solicitações de atualização de dados que estão no final da fila talvez sejam descartadas se coincidirem com o próximo intervalo de processamento.  
  
 Dependendo do suporte oferecido por seu hardware, você poderá atenuar esse problema especificando que processadores adicionais executem um maior número de trabalhos de atualização de dados em paralelo. Para obter mais informações, consulte [configurar dedicado de atualização de dados ou processamento Query-Only &#40;PowerPivot para SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md). Para obter mais informações sobre como as solicitações de atualização de dados são descobertas, adicionadas a uma fila e processadas, consulte [atualização de dados PowerPivot](power-pivot-sharepoint/power-pivot-data-refresh.md).  
  
1.  Na Administração Central, clique em **Monitoramento**.  
  
2.  Clique em **Revisar Definições de Trabalho**.  
  
3.  Selecione o **Trabalho de Timer da Atualização de Dados do PowerPivot**.  
  
4.  Modifique a frequência da agenda para alterar a frequência com que o trabalho de timer examina as informações da agenda da atualização de dados.  
  
##  <a name="bkmk_disableDR"></a> Desabilitar o trabalho de Timer de atualização de dados  
 O trabalho de timer da atualização de dados PowerPivot é um trabalho de timer no nível de farm que é habilitado ou desabilitado para todas as instâncias do servidor PowerPivot no farm. Ele não está ligado a um aplicativo Web ou a um aplicativo do serviço PowerPivot específico. Não é possível desabilitá-lo em alguns servidores para forçar o processamento da atualização de dados em outros servidores do farm.  
  
 Se você desabilitar o trabalho de timer da atualização de dados PowerPivot, as solicitações que já estavam na fila serão processadas, mas nenhuma nova solicitação será adicionada até que você habilite novamente o trabalho. As solicitações que estavam agendadas para ocorrer no passado não são processadas.  
  
 Desabilitar o trabalho de timer não tem nenhum efeito na disponibilidade de recursos nas páginas do aplicativo. Não há nenhuma maneira de remover ou ocultar o recurso de atualização de dados em aplicativos Web. Os usuários que têm permissões de Colaboração ou superior ainda poderão criar novas agendas para operações de atualização de dados, mesmo que o trabalho de timer seja desabilitado permanentemente.  
  
## <a name="see-also"></a>Consulte também  
 [Agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Configurar o processamento de somente consulta ou atualização de dados dedicado &#40;PowerPivot para SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)   
 [Configurar o PowerPivot conta de atualização de dados autônoma &#40;PowerPivot para SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [Configurar credenciais armazenadas para atualização de dados do PowerPivot do &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
