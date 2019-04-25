---
title: Conectar-se ao banco de dados modelo Tabular (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 983d0c8a-77da-4c6e-8638-283bcb14f143
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0f278f5d0d036bac02e53263acc023dcae7d808
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757623"
---
# <a name="connect-to-a-tabular-model-database-ssas"></a>Conectar a um banco de dados de modelo de tabela (SSAS)
  Após criar um modelo de tabela e implantá-lo em um servidor de modo de tabela do Analysis Services, você precisará definir permissões que o disponibilizem para aplicativos cliente. Este tópico explica como conceder permissões e como conectar-se a um banco de dados de aplicativos cliente.  
  
> [!NOTE]  
>  Por padrão, conexões remotas ao Analysis Services não estarão disponíveis até que você configure o firewall. Verifique se abriu a porta apropriada se estiver configurando uma instância nomeada ou padrão para conexões de cliente. Para obter mais informações, consulte [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 Este tópico contém as seguintes seções:  
  
 [Permissões de usuário no banco de dados](#bkmk_userpermissions)  
  
 [Permissões administrativas no servidor](#bkmk_admin)  
  
 [Conectando do Excel ou SharePoint](#bkmk_excelconn)  
  
 [Solucionando problemas de conexão](#bkmk_Tshoot)  
  
##  <a name="bkmk_userpermissions"></a> Permissões de usuário no banco de dados  
 Usuários que conectam-se a bancos de dados de tabela devem ter associação em uma função de banco de dados que especifica o acesso de leitura.  
  
 Funções, e às vezes associação de função, são definidas quando um modelo é criado no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], ou para modelos implantados, usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre como criar funções usando o Gerenciador de Funções no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], consulte [Criar e gerenciar funções &#40;SSAS tabular&#41;](roles-ssas-tabular.md). Para obter mais informações sobre como criar e gerenciar funções para um modelo implantado, consulte [Funções de modelo de tabela &#40;SSAS tabular&#41;](tabular-model-roles-ssas-tabular.md).  
  
> [!CAUTION]  
>  Reimplantar um projeto de modelo de tabela com funções definidas usando o Gerenciador de Função no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] substituirá as funções definidas em um modelo de tabela implantado.  
  
##  <a name="bkmk_admin"></a> Permissões administrativas no servidor  
 Para organizações que usam o SharePoint e Serviços do Excel para hospedar pastas de trabalho do Excel ou relatórios do Reporting Services, uma configuração adicional é necessária para disponibilizar os dados de modelo de tabela para os usuários do SharePoint. Se você não estiver usando o SharePoint, ignore esta seção.  
  
 A exibição de pastas de trabalho do Excel ou relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] que contêm dados de tabela exige que a conta usada para executar Serviços do Excel ou Reporting Services tenha permissões de administrador na instância do Analysis Services. São necessárias permissões administrativas para que esses serviços sejam confiáveis pela instância do Analysis Services.  
  
#### <a name="grant-administrative-access-on-the-server"></a>Conceder o acesso administrativo no servidor  
  
1.  Na Administração Central, abra a página Configurar contas de serviço.  
  
2.  Selecione o pool de aplicativos de serviço usados por Serviços do Excel. Ele pode ser **Pool de aplicativos de serviço - sistema de serviços Web do SharePoint** ou um pool de aplicativos personalizados. A conta gerenciada usada por Serviços do Excel aparecerá na página.  
  
     Para farms do SharePoint que incluem o Reporting Services em modo do SharePoint, obtenha as informações de conta também para o aplicativo de serviço do Reporting Services.  
  
     Nas etapas a seguir, você acrescentará estas contas à função de Servidor na instância do Analysis Services.  
  
3.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], clique com o botão direito do mouse na instância do servidor e selecione **Propriedades**. No Pesquisador de Objetos, clique com o botão direito do mouse em **Funções** e selecione **Nova Função**.  
  
4.  Na página Propriedades do Analysis Services, clique em **Segurança**.  
  
5.  Clique em **Adicionar**e depois insira a conta usada por Serviços do Excel, seguido pela conta usada pelo Reporting Services.  
  
##  <a name="bkmk_excelconn"></a> Conectando do Excel ou SharePoint  
 Bibliotecas de cliente que fornecem acesso a bancos de dados do Analysis Services podem ser usadas na conexão a bancos de dados modelo executados em um servidor de modo de tabela. As bibliotecas incluem o provedor OLE DB do Analysis Services, o ADOMD.NET e o AMO.  
  
 O Excel usa o provedor OLE DB. Se você tiver o MSOLAP.4 do SQL Server 2008 R2 (nome de arquivo msolap100.dll, versão 10.50.1600.1), ou o MSOLAP.5 (nome de arquivo msolap110.dll) que é instalado com a versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] do PowerPivot para Excel, terá uma versão que conectará a bancos de dados de tabela.  
  
 Escolha entre as seguintes abordagens para conectar aos bancos de dados modelo a partir do Excel:  
  
-   Crie uma conexão de dados no Excel, usando as instruções fornecidas na próxima seção.  
  
-   Crie um arquivo de conexão de modelo semântico de BI (.bism) no SharePoint que forneça redirecionamento a um banco de dados executado em um servidor de modo de tabela do Analysis Services. Um arquivo de conexão de modelo semântico de BI fornece um comando de clique com o botão direito do mouse que inicia o Excel usando o banco de dados modelo especificado na conexão. Também iniciará o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] se forem instalados os Reporting Services. Para obter mais informações sobre como criar e usar arquivos de conexão de modelo semântico de BI, consulte [Criar uma conexão de modelo semântico de BI com um banco de dados de modelo de tabela](../power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
-   Crie uma fonte de dados compartilhada do Reporting Services que referencia um banco de dados de tabela como a fonte de dados. Você pode criar a fonte de dados compartilhada no SharePoint e pode usá-la para iniciar o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
#### <a name="connect-from-excel"></a>Conecte do Excel  
  
1.  No Excel, na guia **Dados** , em **Obter Dados Externos**, clique em **De Outras Fontes**.  
  
2.  Selecione **Do Analysis Services**.  
  
3.  Em **Nome de Servidor**, especifique a instância do Analysis Services que hospeda o banco de dados. O nome do servidor costuma ser o nome do computador que executa o software do servidor. Se o servidor foi instalado como uma instância nomeada, você deve especificar o nome neste formato: \<servername >\\< instancename\>.  
  
     A instância de servidor deve ser configurada para a implantação autônoma de tabela e a instância de servidor deve ter uma regra de entrada que permita o acesso a ela. Para mais informações, consulte [Determinar o modo de servidor de uma instância do Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md) e [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
4.  Para fazer logon em credenciais, escolha **Usar Autenticação do Windows** se você tem permissões de leitura para o banco de dados. Caso contrário, escolha **Use as seguintes credenciais de usuário do Windows**e insira o nome de usuário e senha de uma conta do Windows que tenha permissões de banco de dados. Clique em **Avançar**.  
  
5.  Selecione o banco de dados. Uma seleção válida mostrará um único cubo **Modelo** para o banco de dados. Clique em **Avançar** e em **Concluir**.  
  
 Depois que a conexão é estabelecida, você pode usar os dados para criar uma Tabela Dinâmica ou um Gráfico Dinâmico. Para obter mais informações, consulte [Analisar no Excel &#40;SSAS de Tabela&#41;](analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_sharepoint"></a> Conectar do SharePoint  
 Se você estiver usando o PowerPivot para SharePoint, poderá criar um arquivo de conexão de modelo semântico de BI no SharePoint que forneça redirecionamento a um banco de dados executado em um servidor de modo de tabela do Analysis Services. Uma conexão de modelo semântico de BI fornece um ponto de extremidade HTTP a um banco de dados. Isso também simplifica o acesso a modelo de tabela para trabalhadores do conhecimento que costumam usar documentos em um site do SharePoint. Trabalhadores do conhecimento só precisam saber o local do arquivo de conexão de modelo semântico de BI ou sua URL para acessar bancos de dados de modelo de tabela. Detalhes sobre o local do servidor ou o nome do banco de dados são encapsulados na conexão de modelo semântico de BI. Para obter mais informações sobre como criar e usar arquivos de conexão de modelo semântico de BI, consulte [Conexão de modelo semântico do PowerPivot BI &#40;. bism&#41; ](../power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md) e [criar uma Conexão de modelo semântico do BI para um modelo de tabela Banco de dados](../power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
##  <a name="bkmk_Tshoot"></a> Solucionando problemas de conexão  
 Esta seção apresenta a causa e etapas de resolução de problemas que ocorrem na conexão a um banco de dados de modelo de tabela.  
  
 **O Assistente de Conexão de Dados não pode obter uma lista de bancos de dados da fonte de dados especificada.**  
  
 Na importação de dados, este erro do Microsoft Excel ocorre quando você tenta usar o Assistente para se conectar a um banco de dados de modelo de tabela em um servidor remoto do Analysis Services, e você não tem permissões suficientes. Para resolver este erro, você deve ter direitos de acesso de usuário no banco de dados. Consulte as instruções apresentadas antes neste tópico para conceder acesso do usuário aos dados.  
  
 **Ocorreu um erro durante uma tentativa de estabelecer uma conexão à fonte de dados externa. As seguintes conexões não foram atualizadas: \<nome do modelo > área restrita**  
  
 No SharePoint, este erro do Microsoft Excel ocorre quando você tenta a interação de dados, como a filtragem de dados, em uma Tabela Dinâmica que usa dados modelo. O erro ocorre porque você não tem permissões suficientes no servidor remoto do Analysis Services. Para resolver este erro, você deve ter direitos de acesso de usuário no banco de dados. Consulte as instruções apresentadas antes neste tópico para conceder acesso do usuário aos dados.  
  
 **Ocorreu um erro durante a tentativa de executar esta operação. Recarregar a pasta de trabalho e, em seguida, tente executar esta operação novamente.**  
  
 No SharePoint, este erro do Microsoft Excel ocorre quando você tenta a interação de dados, como a filtragem de dados, em uma Tabela Dinâmica que usa dados modelo. O erro ocorre porque os Serviços do Excel não são confiáveis para a instância do Analysis Services na qual os dados modelo são implantados. Para resolver este erro, conceda permissão administrativa de Serviços do Excel na instância do serviço Analysis Services. Consulte as instruções apresentadas antes neste tópico para conceder permissões de administrador. Se o erro persistir, recicle o pool de aplicativos de Serviços do Excel.  
  
 **Erro ao tentar estabelecer uma conexão com a fonte de dados externa usada na pasta de trabalho.**  
  
 No SharePoint, este erro do Microsoft Excel ocorre quando você tenta a interação de dados, como a filtragem de dados, em uma Tabela Dinâmica que usa dados modelo. O erro ocorre porque o usuário não tem permissões do SharePoint suficientes na pasta de trabalho. O usuário deve ter permissões de **Leitura** ou superior. Permissões**Exibir Apenas** não são suficientes para o acesso a dados.  
  
## <a name="see-also"></a>Consulte também  
 [Implantação de uma solução de modelo de tabela &#40;SSAS de Tabela&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
