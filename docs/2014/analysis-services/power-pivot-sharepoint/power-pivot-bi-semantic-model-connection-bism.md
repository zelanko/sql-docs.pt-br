---
title: Conexão de modelo semântico de BI do PowerPivot (. bism) | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 08828eec-4f8c-4f34-a145-e442f7b7031d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 846998acaa20b572760edcc67ecd24f8346a762a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071379"
---
# <a name="powerpivot-bi-semantic-model-connection-bism"></a>Conexão de modelo semântico de BI (.bism) do PowerPivot
  Uma conexão de modelo semântico de BI (.bism) é uma conexão portátil que conecta o Excel ou [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] reporta a um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados modelo de tabela ou uma instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo multidimensional. Se você estiver familiarizado com arquivos de conexão de dados (.odc) do Office, observará uma semelhança em como um arquivo de conexão .bism é definido e usado.  
  
 Uma conexão de modelo semântico de BI é criada e acessada pelo SharePoint. A criação de conexões de modelo semântico de BI habilita comandos de início rápido em uma conexão de modelo semântico de BI em uma biblioteca. Os comandos de início rápido abrem uma nova pasta de trabalho do Excel ou opções para editar o arquivo de conexão. Se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estiver instalado, você também verá um comando para criar um relatório [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 ![Comando de início rápido de captura de tela de BISM](../media/ssas-bism-quicklaunch.gif "comando de início rápido de captura de tela de BISM")  
  
##  <a name="bkmk_prereq"></a> Bancos de dados com suporte  
 Um modelo de conexão semântica de BI aponta para dados de modelo de tabela. Há duas fontes para estes dados:  
  
-   Um banco de dados de modelo de tabela que é executado em uma instância do Analysis Services autônoma em modo de servidor de tabela. Uma implantação de uma instância autônoma do Analysis Services é externa ao farm. Acessando fontes de dados fora do farm requer permissões adicionais, o qual você pode ler neste tópico: [Criar uma Conexão de modelo semântico de BI para um banco de dados do modelo de tabela](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
-   Pastas de trabalho PowerPivot salvas no SharePoint. Bancos de dados PowerPivot inseridos em pastas de trabalho do Excel são equivalentes a bancos de dados de modelo de tabela que são executados em um servidor autônomo de modo de tabela do Analysis Services. Se você já usa o PowerPivot para Excel e o PowerPivot para SharePoint, poderá definir uma conexão de modelo semântico de BI que aponte para pastas de trabalho PowerPivot em uma biblioteca do SharePoint e compilar relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] usando dados PowerPivot existentes.  Você pode usar pastas de trabalho criadas na versão SQL Server 2008 R2 ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] do PowerPivot para Excel.  
  
-   Um modelo de dados multidimensionais em uma instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Para obter uma comparação das fontes de dados, consulte o conteúdo da comunidade [Understanding the SQL Server 2012 BI Semantic Model (BISM) (Entendendo o BISM (modelo semântico de BI) do SQL Server 2012)](http://www.mssqltips.com/sqlservertip/2818/understanding-the-sql-server-2012-bi-semantic-model-bism/).  
  
## <a name="understanding-the-connection-sequence-for-bi-semantic-connections"></a>Entendendo a sequência de conexão para conexões semânticas de BI  
 Esta seção explica o comportamento da conexão entre vários aplicativos cliente, como o aplicativo de área de trabalho do Excel ou o cliente de relatório do Power View no SharePoint e um banco de dados modelo de tabela dentro ou fora do farm do SharePoint.  
  
 Todas as conexões com um banco de dados modelo de tabela são estabelecidas com o uso de credenciais do usuário que está solicitando os dados. No entanto, a mecânica dessas conexões variará dependendo se a conexão está dentro do farm, se é do tipo de salto único ou duplo e se o Kerberos está habilitado. Para obter mais informações sobre conexões autenticadas entre fontes de dados do SharePoint e o back-end, consulte [autenticação de salto duplo: Por que o NTLM falha e o Kerberos funciona](https://go.microsoft.com/fwlink/?LinkId=237137).  
  
 **Conectando do Excel a dados de tabela em uma rede**  
  
 Quando um usuário do Excel especifica uma conexão de modelo de semântica de BI como a fonte de dados, as informações de conexão dentro do arquivo .bism são baixadas para o aplicativo de cliente, que, em seguida, emite sua própria solicitação direta para o banco de dados modelo de tabela no Analysis Services. Para acessar a conexão .bism, o usuário do Excel deve ser um usuário do SharePoint com permissões de leitura no arquivo de conexão .bism. Quando as informações de conexão são baixadas, todas as conexões subsequentes ignoram o SharePoint, fluindo diretamente do Excel para o banco de dados modelo de tabela de back-end.  
  
 A ilustração a seguir mostra esta sequência de conexão. Ela começa com uma solicitação para a conexão .bism, seguida pelo download das informações de conexão com o cliente e, finalmente, a conexão de salto único com o banco de dados. A conexão é estabelecida usando-se as credenciais do Windows do usuário do Excel que tem permissões de leitura no banco de dados do Analysis Services. Trata-se de um salto único, portanto, mesmo que o Kerberos esteja habilitado, ele não é necessário para esse cenário.  
  
 ![Conexões do Excel para o banco de dados modelo tabular](../media/ssas-powerpivotbismconnection-1.gif "conexões do Excel ao banco de dados de modelo de tabela")  
  
 **Conectando do Power View a dados de tabela em uma rede**  
  
 Quando um usuário do SharePoint clica em uma conexão semântica de BI em uma biblioteca de documentos, o Power View (se estiver instalado) é iniciado automaticamente e estabelece uma conexão com o banco de dados modelo de tabela.  
  
 Conexões entre o Power View e um banco de dados modelo de tabela seguem uma sequência de autenticação de salto duplo na qual a identidade do usuário flui do cliente para o SharePoint e depois do SharePoint para um banco de dados modelo de tabela de back-end do Analysis Services que é executado fora do farm. A biblioteca cliente ADOMD.NET que manipula a solicitação de conexão sempre tenta o Kerberos primeiro. Se o Kerberos estiver configurado, a identidade do usuário será representada na conexão com o banco de dados modelo de tabela e a conexão será bem-sucedida.  
  
 Se o Kerberos não estiver configurado e a solicitação falhar, o Reporting Services fará uma segunda tentativa. Neste cenário, a biblioteca cliente se conectará ao Analysis Services usando a identidade de serviço do Reporting Services e a autenticação NTLM. A identidade do Power View é passada na cadeia de conexão usando o parâmetro `effectiveusername`.  
  
 Somente um membro da função de administrador do sistema na instância do Analysis Services tem permissão para estabelecer uma conexão usando o parâmetro `effectiveusername` e representar outro usuário na instância do servidor. Por isso, a conta de execução do serviço compartilhado do Reporting Services deve ter direitos administrativos na instância do Analysis Services.  Instruções sobre como conceder permissões administrativas à conta de serviço são fornecidas neste tópico [Criar uma conexão de modelo semântico de BI com um banco de dados de modelo de tabela](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
 A ilustração a seguir mostra uma sequência de conexão que usa a mesma identidade de usuário do Windows para cada conexão. Na última conexão com o Analysis Services, ela é estabelecida pela identidade do aplicativo de serviço do Reporting Services, passando a identidade de usuário do Windows usando `effectiveusername`.  
  
 ![Conexão representada para BD tabular](../media/ssas-powerpivotbismconnection-2.gif "conexão representada para BD tabular")  
  
 **Conectando do Power View para dados PowerPivot no SharePoint**  
  
 Quando um usuário do SharePoint clica em uma conexão semântica de BI que se resolve para uma pasta de trabalho PowerPivot no mesmo farm, as conexões ocorrem no contexto do ambiente do SharePoint. Um aplicativo de serviço PowerPivot manipula a solicitação de conexão, que encaminha à instância do Analysis Services no mesmo computador. A instância do Analysis Services extrai os dados PowerPivot da pasta de trabalho e carrega-os. Todas as conexões subsequentes são gerenciadas por aplicativos de serviço PowerPivot no farm.  
  
 Neste cenário, todas as conexões ocorrem dentro do mesmo farm, assim não há nenhum requisito para Kerberos ou delegação restrita.  
  
##  <a name="bkmk_rel"></a> Tarefas relacionadas  
 [Adicionar um tipo de conteúdo de Conexão de modelo semântico BI em uma biblioteca do &#40;PowerPivot para SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)  
  
 [Criar uma conexão de modelo semântico de BI para uma pastas de trabalho PowerPivot](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [Criar uma conexão de modelo semântico de BI com um banco de dados de modelo de tabela](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
 [Usar uma conexão de modelo semântico de BI no Excel ou Reporting Services](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Conectar ao Analysis Services](../instances/connect-to-analysis-services.md)  
  
  
