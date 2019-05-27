---
title: Criar uma Conexão de modelo semântico de BI para um banco de dados de modelo Tabular | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 69b306f6-ee8a-44d2-8f51-0cad2c0bc135
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f058516059c0cadf92b9d558a47990af0a54725f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071658"
---
# <a name="create-a-bi-semantic-model-connection-to-a-tabular-model-database"></a>Criar uma conexão de modelo semântico de BI com um banco de dados de modelo de tabela
  Use as informações neste tópico para configurar uma conexão de modelo semântico de BI que redireciona para um banco de dados modelo de tabela em execução em uma instância do Analysis Services fora do farm do SharePoint.  
  
 Depois de criar uma conexão de modelo semântico de BI e configurar o SharePoint e as permissões do Analysis Services, as pessoas podem usá-lo como uma fonte de dados para Excel ou relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 Este tópico inclui as seções a seguir. Execute cada tarefa na ordem fornecida.  
  
 [Examinar pré-requisitos](#bkmk_prereq)  
  
 [Conceder permissões administrativas do Analysis Services para os Aplicativos de Serviços Compartilhados](#bkmk_ssas)  
  
 [Conceder permissões de leitura no banco de dados de modelo de tabela](#bkmk_BISM)  
  
 [Criar uma conexão de modelo semântico de BI com um banco de dados de modelo de tabela](#bkmk_connect)  
  
 [Configurar permissões de SharePoint na conexão de modelo semântico de BI](#bkmk_permissions)  
  
 [Próximas etapas](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> Examinar pré-requisitos  
 É necessário ter permissões Colaborar ou superior para criar um arquivo de conexão de modelo semântico de BI.  
  
 Você deve ter uma biblioteca que dá suporte ao tipo de conteúdo da conexão de modelo semântico de BI. Para obter mais informações, consulte [adicionar um tipo BI Semantic modelo Conexão conteúdo em uma biblioteca do &#40;PowerPivot para SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md).  
  
 Você deve saber o servidor e o nome de banco de dados para os quais está configurando uma conexão de modelo semântico de BI. O Analysis Services deve ser configurado para modo de tabela. Os bancos de dados que são executados no servidor devem ser bancos de dados de modelo de tabela. Para obter instruções sobre como verificar o modo de servidor, consulte [Determinar o modo de servidor de uma instância do Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Em certos cenários, os serviços compartilhados em um ambiente do SharePoint devem ter permissões administrativas na instância do Analysis Services. Esses serviços incluem aplicativos de serviço PowerPivot, aplicativos de serviço Reporting Services e o serviço PerformancePoint. Antes de poder conceder permissões administrativas, você deve saber a identidade desses aplicativos de serviço. Você pode usar a Administração Central para determinar a identidade.  
  
 Você deve ser administrador de serviço do SharePoint para exibir informações de segurança em Administração Central.  
  
 Você deve ser administrador de sistema do Analysis Services para conceder direitos administrativos no Management Studio.  
  
 O PowerPivot para SharePoint deve ser acessado por aplicativos Web que utilizam o modo de autenticação clássico. As conexões de modelo semântico de BI para fontes de dados externas têm uma dependência do logon do modo clássico. Para obter mais informações, consulte [PowerPivot Authentication and Authorization](power-pivot-authentication-and-authorization.md).  
  
 Todos os computadores e usuários que participam da sequência de conexão devem estar no mesmo domínio ou domínio confiável (confiança bidirecional).  
  
##  <a name="bkmk_ssas"></a> Conceder permissões administrativas do Analysis Services para os Aplicativos de Serviços Compartilhados  
 As conexões que se originam do SharePoint para um banco de dados modelo de tabela em um servidor do Analysis Services são feitas, às vezes, por um serviço compartilhado em nome do usuário que solicita os dados. O serviço que faz a solicitação pode ser um aplicativo de serviço PowerPivot, um aplicativo de serviço Reporting Services ou um aplicativo de serviço PerformancePoint. Para que a conexão seja bem-sucedida, o serviço deve ter permissões administrativas no servidor do Analysis Services. No Analysis Services, somente um administrador tem permissão de fazer uma conexão representada em nome de outro usuário.  
  
 As permissões administrativas são necessárias quando a conexão é usada sob estas condições:  
  
-   Ao verificar as informações de conexão durante a configuração de um arquivo de conexão de modelo semântico de BI.  
  
-   Ao iniciar um relatório do Power View usando uma conexão de modelo semântico de BI.  
  
-   Ao popular uma Web Part do PerformancePoint usando uma conexão de modelo semântico de BI.  
  
 Para assegurar que esses comportamentos sejam executados como esperado, conceda a cada identidade de serviço permissões administrativas na instância do Analysis Services. Use as instruções a seguir para conceder a permissão necessária.  
  
 **Adicione identidades de serviço à função de Administrador de Servidor**  
  
1.  No SQL Server Management Studio, conecte-se à instância do Analysis Services.  
  
2.  Clique com o botão direito do mouse no nome do servidor e selecione **Propriedades**.  
  
3.  Clique em **Segurança**, depois em **Adicionar**. Insira a conta de usuário do Windows que é usada para executar o aplicativo de serviço.  
  
     Você pode usar a Administração Central para determinar a identidade. Na seção Segurança, abra **Configurar contas de serviço** para visualizar qual conta do Windows está associada ao pool de aplicativos de serviço usado para cada aplicativo e siga as instruções fornecidas neste tópico para conceder permissões administrativas à conta.  
  
##  <a name="bkmk_BISM"></a> Conceder permissões de leitura no banco de dados de modelo de tabela  
 Como o banco de dados está sendo executado em um servidor que é externo ao farm, parte de configurar suas conexões incluirá conceder permissões de usuário de banco de dados no servidor do Analysis Services de back-end. O Analysis Services usa um modelo de permissão baseado em função. Usuários que conectam a bancos de dados modelo devem fazer isso com permissões de leitura ou superiores, através de uma função que conceda acesso de leitura a seus membros.  
  
 Funções, e às vezes associação de função, são definidas quando o modelo é criado no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Você não pode usar o SQL Server Management Studio para criar funções, mas pode usá-lo para adicionar membros a uma função que já esteja definida. Para obter mais informações sobre como criar funções, consulte [Criar e gerenciar funções &#40;SSAS Tabular&#41;](../tabular-models/roles-ssas-tabular.md).  
  
#### <a name="assign-role-membership"></a>Atribuir associação de função  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda o banco de dados no Pesquisador de Objetos e expanda **Funções**. Você deverá ver uma função que já esteja definida. Se uma função não existir, entre em contato com o autor do modelo e solicite a adição ou uma função. O modelo deve ser reimplantado antes de a função estar visível no Management Studio.  
  
2.  Clique com o botão direito do mouse na função e selecione **Propriedades**.  
  
3.  Na página Associação, adicione as contas de grupo e usuário do Windows que requerem acesso.  
  
##  <a name="bkmk_connect"></a> Criar uma conexão de modelo semântico de BI com um banco de dados de modelo de tabela  
 Depois de definir permissões no Analysis Services, você poderá voltar para o SharePoint e criar uma conexão de modelo semântico de BI.  
  
1.  Na biblioteca que conterá a conexão de modelo semântico de BI, clique em **Documentos** na faixa de opções do SharePoint.  
  
2.  Clique na seta para baixo em Novo Documento e selecione **Arquivo de Conexão de Modelo Semântico de BI** para abrir uma nova página de Conexão de Modelo Semântico de BI.  
  
3.  Defina as propriedades **Server** e **Database** . Se estiver incerto quanto ao nome do banco de dados, use o SQL Server Management Studio para exibir uma lista dos bancos de dados implantados no servidor.  
  
     **Nome do servidor** é o nome de rede do servidor, o endereço IP ou o nome de domínio totalmente qualificado (por exemplo, myserver.mydomain.corp.adventure-works.com). Se o servidor estiver instalado como uma instância nomeada, insira o nome do servidor neste formato: computername\instancename.  
  
     **Banco de dados** deve ser um banco de dados de tabela que está disponível atualmente no servidor. Não especifique outro arquivo de conexão de modelo semântico de BI, um arquivo .odc (conexão de dados do Office), um banco de dados OLAP do Analysis Services ou uma pasta de trabalho PowerPivot. Para obter o nome do banco de dados, você pode usar o Management Studio para conectar-se ao servidor e exibir a lista de bancos de dados disponíveis. Use a página de propriedades do banco de dados para verificar se você tem o nome correto.  
  
4.  Clique em **OK** para salvar a página. Nesse momento, o aplicativo de serviço PowerPivot verificará a conexão.  
  
     A verificação será bem-sucedida se as informações de conexão estiverem corretas e você tiver concedido permissões administrativas ao aplicativo de serviço PowerPivot, para que ele possa se conectar ao Analysis Services como o usuário atual.  
  
     A verificação falhará se as informações de conexão estiverem erradas ou se o aplicativo de serviço carecer de permissões. Uma mensagem de validação aparecerá na página perguntando se você deseja salvar o arquivo. Se você souber que a conexão é válida, deverá salvar o arquivo assim mesmo, pois o erro é decorrente da falta de permissões, e não das informações de conexão inválidas.  
  
     Você poderá verificar a conexão usando isso no Excel ou Power View para se conectar ao banco de dados modelo de tabela. Se a conexão de fonte de dados for bem-sucedida, a conexão será válida apesar do aviso de verificação.  
  
##  <a name="bkmk_permissions"></a> Configurar permissões de SharePoint na conexão de modelo semântico de BI  
 A capacidade para usar uma conexão de modelo semântico de BI como uma fonte de dados para uma pasta de trabalho do Excel ou relatório do Reporting Services exige permissões de **Leitura** no item de conexão do modelo semântico de BI em uma biblioteca do SharePoint. O nível de permissão de leitura inclui a permissão **Abrir Itens** que habilita o carregamento de informações da conexão de modelo semântico de BI em um aplicativo de área de trabalho do Excel.  
  
 Há várias maneiras de conceder permissões no SharePoint. As instruções a seguir explicam como criar um novo grupo chamado **Usuários do BISM** que tem o nível de permissão de **Leitura** .  
  
 Você deve ser proprietário do site para alterar permissões.  
  
1.  Em Ações do Site, clique em **Permissões do Site**.  
  
2.  Clique em **Criar Grupo** e dê o nome de **Usuários do BISM**ao novo grupo.  
  
3.  Escolha o nível de permissão de **Leitura** e clique em **Criar**.  
  
4.  Selecione **Usuários do BISM** em Pessoas e Grupos.  
  
5.  Aponte para Novo, clique em **Adicionar Usuários**e adicione contas de usuário ou grupo.  
  
     Estes usuários e grupos agora terão permissões de Leitura em todo o site, incluindo todas as bibliotecas e listas que herdam permissões do nível do site. Se estas permissões forem muito altas, você poderá remover este grupo seletivamente de bibliotecas específicas, listas ou itens.  
  
 Para remover permissões seletivamente no nível do item, faça o seguinte:  
  
1.  Em uma biblioteca, selecione um documento. Clique na seta para baixo à direita e clique em **Gerenciar Permissões**.  
  
2.  Por padrão, um item herda permissões. Para alterar as permissões de documentos individuais nessa biblioteca, clique em **Parar de Herdar Permissões**.  
  
3.  Marque a caixa de seleção junto a **Usuários do BISM**.  
  
4.  Clique em **Remover Permissões do Usuário**.  
  
##  <a name="bkmk_next"></a> Próximas etapas  
 Depois de criar e proteger uma conexão de modelo semântico de BI, você poderá especificá-la como uma fonte de dados. Para obter mais informações, consulte [Usar uma conexão de modelo semântico de BI no Excel ou Reporting Services](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conexão de modelo semântico de BI do PowerPivot &#40;. bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [Criar uma conexão de modelo semântico de BI para uma pastas de trabalho PowerPivot](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
  
