---
title: Agendar uma atualização de dados (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 8571208f-6aae-4058-83c6-9f916f5e2f9b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1cfbd8496a700f03ae91e81f1fcf442c1a12bcfa
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84538918"
---
# <a name="schedule-a-data-refresh-powerpivot-for-sharepoint"></a>Agendar uma atualização de dados (PowerPivot para SharePoint)
  Você pode agendar a atualização de dados para obter atualizações automáticas para dados PowerPivot dentro de uma pasta de trabalho do Excel publicada em um site do SharePoint.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
 **Neste tópico:**  
  
 [Pré-requisitos](#prereq)  
  
 [Visão geral de atualização de dados](#intro)  
  
 [Habilitar e agendar a atualização de dados](#drenablesched)  
  
 [Verificar a atualização de dados](#drverify)  
  
> [!NOTE]  
>  A atualização de dados PowerPivot é executada por instâncias de servidor do Analysis Services no farm do SharePoint. Ela não está relacionada ao recurso de atualização de dados fornecido nos Serviços do Excel. O recurso Agendar atualização de dados do PowePivot não atualizará os dados que não sejam do PowerPivot.  
  
##  <a name="prerequisites"></a><a name="prereq"></a> Pré-requisitos  
 Você precisa ter nível de permissão Colaboração ou superior na pasta de trabalho para criar uma agenda de atualização de dados.  
  
 As fontes de dados externas acessadas durante a atualização de dados devem estar disponíveis e as credenciais especificadas na agenda devem ter permissão para acessar essas fontes de dados. A atualização de dados agendada exige um local da fonte de dados acessível em uma conexão de rede (por exemplo, de um compartilhamento de arquivos de rede e não de uma pasta local em sua estação de trabalho).  
  
 A fonte de dados não pode ser um documento do Office ou um banco de dados do Access. O Office não dá suporte ao uso dos componentes de conectividade de dados Office em um ambiente de servidor. Se sua pasta de trabalho contiver dados dessas fontes, remova-as da lista de fontes de dados em sua agenda de atualização de dados.  
  
 A pasta de trabalho deve ser uma versão do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] . Se você usar pastas de trabalho que foram criadas na versão anterior do PowerPivot para Excel, a atualização de dados de agenda não funcionará a menos que você atualize o banco de dados da versão mais recente.  
  
 O check in da pasta de trabalho deve ser feito quando a operação de atualização for concluída. Um bloqueio na pasta de trabalho é colocado no arquivo ao final da atualização de dados, quando o arquivo é salvo, em vez de quando a atualização é iniciada.  
  
> [!NOTE]  
>  O servidor não bloqueia a pasta de trabalho enquanto a atualização de dados está em andamento. Porém, ele bloqueia o arquivo ao término da atualização de dados para fins de verificação do arquivo atualizado. Se, no momento, o check-out do arquivo for outro usuário, os dados atualizados serão descartados. Da mesma forma, se o check-in do arquivo for feito, mas for significativamente diferente da cópia recuperada pelo servidor no início da atualização de dados, os dados atualizados serão descartados.  
  
##  <a name="data-refresh-overview"></a><a name="intro"></a>Visão geral da atualização de dados  
 Dados PowerPivot em uma pasta de trabalho do Excel podem derivar de várias fontes de dados externas, incluindo bancos de dados externos ou arquivos de dados que você acessa de servidores remotos ou de compartilhamentos de arquivos de rede. Para pastas de trabalho PowerPivot que contêm dados importados de fontes de dados conectadas ou externas, você pode configurar a atualização de dados para agendar uma importação automática de dados atualizados dessas fontes originais.  
  
 Uma fonte de dados externa é acessada por uma cadeia de conexão inserida, URL ou caminho UNC que você especificou quando importou os dados originais para a pasta de trabalho usando o aplicativo cliente PowerPivot. As informações de conexão originais que são armazenadas na pasta de trabalho PowerPivot são reutilizadas para operações de atualização de dados subsequentes. Embora você possa substituir as credenciais usadas para conectar-se a fontes de dados, não é possível substituir cadeias de caracteres de conexão para atualizar dados; são utilizadas apenas as informações de conexão.  
  
 Há apenas uma página de agenda de atualização de dados para cada pasta de trabalho e todas as informações de agenda são especificadas nessa página. Normalmente, a pessoa que criou a pasta de trabalho define a agenda.  
  
 Como proprietário da agenda, você executa as seguintes tarefas:  
  
-   Defina a agenda padrão. Isto é, a agenda que será usada se não houver nenhum agendamento definido no nível da fonte de dados.  
  
-   Especifique as credenciais usadas para executar a atualização de dados  
  
-   Escolha quais fontes de dados incluir na operação de atualização.  
  
-   Opcionalmente, especifique agendas individuais embutidas e credenciais para cada fonte de dados consultada durante a atualização de dados. Cada fonte de dados pode ser atualizada independentemente. Se você criar agendas personalizadas para cada fonte de dados, a agenda padrão será ignorada.  
  
 A criação de agendas granulares para fontes de dados individuais permite a você coincidir a agenda de atualização com flutuações nas fontes de dados externas. Por exemplo, se uma fonte de dados externa contiver dados transacionais que são gerados ao longo do dia, você poderá criar uma agenda de atualização de dados individual para essa fonte de dados para obter as informações atualizadas toda noite.  
  
##  <a name="enable-and-schedule-data-refresh"></a><a name="drenablesched"></a>Habilitar e agendar atualização de dados  
 Use as instruções a seguir para agendar a atualização de dados para dados do PowerPivot em uma pasta de trabalho do Excel que é publicada em uma biblioteca do SharePoint.  
  
1.  Na biblioteca que contém a pasta de trabalho, selecione a pasta de trabalho e clique na seta para baixo para exibir uma lista de comandos.  
  
2.  Clique em **Gerenciar Atualização de Dados do PowerPivot**. Se uma agenda de atualização de dados já estiver definida, você verá a página de histórico Exibir Atualização de Dados. Você pode clicar em **Configurar atualização de dados** para abrir a página de definição de agenda.  
  
3.  Na página de definição de agenda, selecione a caixa de seleção **Habilitar** .  
  
4.  Em Detalhes de Agenda, especifique o tipo de agenda e os detalhes. Esta etapa cria a agenda padrão.  
  
    > [!IMPORTANT]  
    >  Marque a caixa de seleção **Também atualizar o mais rápido possível** . Isso permite verificar se a atualização de dados é operacional para esta pasta de trabalho. Note que, após você salvar a agenda, a atualização de dados poderá levar até um minuto para iniciar.  
  
5.  Em Hora de Início Mais Antiga, escolha uma das seguintes opções:  
  
    1.  **Depois do horário comercial** especifica um período de processamento fora do expediente, quando é mais provável que os servidores do banco de dados tenham dados atuais que foram gerados no horário comercial.  
  
    2.  **A hora de início mais antiga específica** equivale ao primeiro período de tempo do dia, em hora e minutos, no qual a solicitação de atualização de dados foi adicionada a uma fila de processo. Você pode especificar os minutos em intervalos de 15 minutos. A configuração aplica-se tanto ao dia atual quanto a datas futuras. Por exemplo, se você especificar um valor de 6:30. e a hora atual for 16:30, a solicitação de atualização será adicionada à fila no dia corrente porque 16:30 é posterior à 6:30.  
  
     A hora de início mais antiga define quando uma solicitação é adicionada à fila de processo. O processamento real ocorre quando o servidor tem recursos adequados para começar o processamento de dados. A hora de processamento real será registrada no histórico de atualização de dados quando o processamento for concluído.  
  
6.  Marque a caixa de seleção **Também atualizar o mais rápido possível** para executar a atualização de dados assim que o servidor puder processar isso. Um resultado com êxito de um trabalho de atualização de dados verifica que as fontes de dados estão disponíveis e que permissões e configuração de servidor estão definidas corretamente.  
  
7.  Em Notificações de email, insira o endereço de email da pessoa que deve ser notificada no caso de um erro de processamento.  
  
8.  Em Credenciais, especifique uma conta usada para executar o trabalho de atualização de dados. A conta deve ter permissões Contribuir na pasta de trabalho para poder abri-la para atualizar seus dados. Ela deve ser uma conta de usuário de domínio do Windows. Em muitos casos, essa conta também deve ter permissões de leitura nas fontes de dados externas usadas durante a atualização de dados. Especificamente, se você importou originalmente os dados que usam a opção Usar a Autenticação do Windows, a cadeia de conexão será compilada para usar as credenciais do Windows do usuário atual. Se o usuário atual for a conta de atualização de dados, essa conta deverá ter permissões de leitura na fonte de dados externa para que a atualização de dados tenha êxito. Selecione uma das seguintes opções:  
  
    1.  Escolha **Usar a conta de atualização de dados configurada pelo administrador** para processar a operação de atualização de dados usando a conta de atualização autônoma de dados PowerPivot.  
  
    2.  Escolha **Conectar usando as seguintes credenciais de usuário do Windows** se você desejar inserir um nome de usuário e senha. Insira informações da conta no formato domínio\usuário.  
  
    3.  Escolha **Conecte-se usando as credenciais salvas no Serviço de Repositório Seguro** se souber a ID de um aplicativo de destino que contém as credenciais previamente armazenados que você deseja usar.  
  
     Para obter mais informações sobre essas opções, consulte [configurar credenciais armazenadas para a atualização de dados PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md) e [Configurar a conta de atualização de dados autônoma do PowerPivot &#40;PowerPivot para SharePoint ](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)&#41;.  
  
9. Em Fontes de Dados, marque a caixa de seleção **Todas as fontes de dados** se desejar que a atualização de dados consulte novamente todas as fontes de dados originais.  
  
     Se você selecionar essa opção, qualquer fonte de dados externa que forneça dados PowerPivot será incluída automaticamente na atualização, até mesmo se a lista de fontes de dados mudar com o tempo à medida que você adicionar ou remover fontes de dados que são fornecem dados à pasta de trabalho.  
  
     Desmarque a caixa de seleção **Todas as fontes de dados** se desejar selecionar manualmente as fontes de dados a serem incluídas. Se você modificar posteriormente a pasta de trabalho, adicionando uma nova fonte de dados, atualize a lista de fontes de dados na agenda. Caso contrário, as fontes de dados mais novas não serão incluídas na operação de atualização.  
  
     A lista de fontes de dados que você pode escolher é recuperada da pasta de trabalho PowerPivot quando você abre a página Gerenciar Atualização de Dados PowerPivot para a pasta de trabalho.  
  
     Selecione apenas as fontes de dados que atendam aos seguintes critérios:  
  
    -   A fonte de dados deve estar disponível no momento em que ocorre a atualização de dados e no local indicado. Se a fonte de dados original estiver em uma unidade de disco local da pessoa que criou a pasta de trabalho, você deverá excluir essa fonte de dados da operação de atualização de dados ou encontrar uma forma de publicar essa fonte de dados em um local acessível por uma conexão de rede. Se você transferir uma fonte de dados para um local de rede, abra a pasta de trabalho no [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] e atualize as informações de conexão da fonte de dados. Isso é necessário para restabelecer as informações de conexão que são armazenadas na pasta de trabalho PowerPivot.  
  
    -   A fonte de dados precisa ser acessada usando as informações de credenciais que foram inseridas na pasta de trabalho PowerPivot ou que foram especificadas na agenda. As informações de credenciais inseridas são armazenadas na pasta de trabalho PowerPivot quando você importa dados usando o PowerPivot para Excel. Informações de credenciais inseridas são frequentemente SSPI=IntegratedSecurity ou SSPI=TrustedConnection, o que significa o uso das credenciais do usuário atual para conexão à fonte de dados. Se você desejar anular as informações de credenciais em sua agenda de atualização de dados, poderá especificar credenciais armazenadas, predefinidas. Para obter mais informações, consulte [configurar credenciais armazenadas para a atualização de dados PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
    -   A atualização de dados deve ter êxito para todas as fontes de dados especificadas. Caso contrário, os dados atualizados serão descartados e você ficará com a última versão salva da pasta de trabalho. Exclua qualquer fonte de dados duvidosa.  
  
    -   A atualização de dados não deve invalidar outros dados da sua pasta de trabalho. Quando você atualiza um subconjunto de seus dados, é importante compreender se a pasta de trabalho ainda é válida quando dados mais novos são agregados com dados estáticos que são de períodos diferentes. Como autor de uma pasta de trabalho, cabe a você conhecer suas dependências de dados e garantir que a atualização de dados seja apropriada para a própria pasta de trabalho.  
  
10. Opcionalmente, você pode definir agendas individuais para fontes de dados específicas. Isso é útil quando as próprias fontes de dados originais são atualizadas em uma agenda. Por exemplo, se uma fonte de dados PowerPivot usar dados de um data mart que é atualizado toda segunda-feira às 02:00 horas, você poderá definir uma agenda interna para o data mart a fim de recuperar seus dados atualizados toda segunda-feira às 04:00 horas.  
  
11. Clique em **OK** para salvar sua agenda.  
  
##  <a name="verify-data-refresh"></a><a name="drverify"></a>Verificar atualização de dados  
 A melhor forma de verificar a atualização de dados é executar logo a atualização de dados e depois analisar a página de histórico para verificar se ela foi concluída com êxito. Quando a caixa de seleção **Também atualizar o mais rápido possível** é marcada na sua agenda, isso permite verificar que a atualização de dados é operacional.  
  
 Você pode exibir o registro atual e anterior de operações de atualização de dados na página Histórico de Atualização de Dados da pasta de trabalho. Essa página só aparecerá se a atualização de dados tiver sido agendada para uma pasta de trabalho. Se não houver agenda de atualização de dados, a página de definição de agenda aparecerá.  
  
 Você precisa ter permissões de Colaboração ou superiores para exibir o histórico de atualização de dados.  
  
1.  Em um site do SharePoint, abra a biblioteca contendo uma pasta de trabalho PowerPivot.  
  
     Não há indicador visual que identifique quais pastas de trabalho em uma biblioteca do SharePoint contêm dados PowerPivot. Você deve saber previamente quais pastas de trabalho contêm dados atualizáveis do PowerPivot.  
  
2.  Selecione o documento e clique na seta para baixo exibida à direita.  
  
3.  Selecione **Gerenciar Atualização de Dados PowerPivot**.  
  
 A página de histórico é exibida, mostrando um registro completo de todas as atividades de atualização de dados PowerPivot na pasta de trabalho atual do Excel, incluindo o status da operação mais recente de atualização de dados.  
  
 Em alguns casos, talvez você encontre um tempo real de processamento diferente do tempo especificado por você. Isso ocorrerá se a carga de processamento no servidor for pesada. Quando a carga é pesada, a instância de serviço do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] aguarda até a liberação de uma quantidade suficiente de recursos do sistema antes de começar uma atualização dos dados.  
  
 É necessário submeter a pasta de trabalho a check-in quando a operação de atualização é concluída. A pasta de trabalho será salva com os dados atualizados naquele momento. Se for realizado o check-out no arquivo, a atualização de dados será ignorada até a próxima hora agendada.  
  
 Se você encontrar uma mensagem de status inesperada (por exemplo, falha ou cancelamento de uma operação de atualização), poderá investigar o problema verificando permissões e a disponibilidade do servidor.  
  
 Revise a página de solução de problemas de atualização de dados PowerPivot no WIKI do TechNet para obter ajuda sobre o assunto. Para obter mais informações, consulte [Solucionando problemas de atualização de dados PowerPivot](https://go.microsoft.com/fwlink/?LinkId=251594).  
  
> [!NOTE]  
>  Os administradores do SharePoint podem ajudá-lo a solucionar problemas de atualização de dados exibindo os relatórios de atualização de dados consolidados no Painel de Gerenciamento do PowerPivot na Administração Central. Para obter mais informações, consulte [PowerPivot Management Dashboard and Usage Data](power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Atualização de dados PowerPivot com o SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [Exibir o histórico de atualização de dados &#40;PowerPivot para SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)   
 [Configurar credenciais armazenadas para a atualização de dados do PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
