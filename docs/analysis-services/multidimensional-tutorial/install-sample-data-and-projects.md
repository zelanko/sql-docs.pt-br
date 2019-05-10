---
title: Instalar dados de exemplo do Analysis Services e projetos | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 999e1c1434bd727fe0ac889c2041145a5c1ec750
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404088"
---
# <a name="install-sample-data-and-multidimensional-projects"></a>Instalar dados de exemplo e projetos multidimensionais 
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

Use as instruções e links fornecidos neste artigo para instalar os arquivos de projeto e os dados usados em tutoriais do Analysis Services. 
  
## <a name="step-1-install-prerequisites"></a>Etapa 1: Instalar pré-requisitos 
As lições neste tutorial presumem que você tenha o seguinte software instalado. Você pode instalar todos os recursos em um único computador. Para instalar estes recursos, execute a Instalação do SQL Server e selecione-os na página Seleção de Recursos.  
  
-   Mecanismo de Banco de Dados do SQL Server  
  
-   SQL Server Analysis Services  (SSAS) 
  
    Analysis Services está disponível apenas nestas edições: Evaluation, Enterprise, Business Intelligence, Standard. Não há suporte para modelos multidimensionais no Azure Analysis Services.
  
    Por padrão, o Analysis Services 2016 e posterior é instalado como uma instância de tabela, você pode substituir escolhendo modo Multidimensional do servidor no servidor de página de configuração do Assistente de instalação.
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>Etapa 2: Baixe e instale as ferramentas para desenvolvimento e gerenciamento
SQL Server Data Tools (SSDT) para o Visual Studio é baixado e instalado separadamente de outros recursos do SQL Server. Os designers e modelos de projeto usados para criar modelos de BI e relatórios estão incluídos no SSDT para Visual Studio 2015 ou como [pacotes do Nuget](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) para Visual Studio 2017.  
  
[Baixar o SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542).   

SQL Server Management Studio (SSMS) é baixado e instalado separadamente de outros recursos do SQL Server.  

[Baixar o SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)  

Como opção, instale o Excel para procurar seus dados multidimensionais à medida que você continua pelo tutorial. A instalação do Excel habilita o recurso **Analisar no Excel** que inicia o Excel usando uma lista de campo de Tabela Dinâmica que é conectada ao cubo que está sendo criado. Usar o Excel para procurar dados é recomendado porque você pode rapidamente criar um relatório dinâmico que permite interagir com os dados.  
  
Como alternativa, você pode procurar dados usando o designer de consulta MDX interno que é embutido no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. O criador de consultas retorna os mesmos dados, menos os que são apresentados como um conjunto de linhas simples.  
  
## <a name="step-3-install-databases"></a>Etapa 3: Instalar bancos de dados  
Um modelo multidimensional do Analysis Services usa dados transacionais que você importa de um RDBMS. Para os fins deste tutorial, você pode usar o seguinte banco de dados relacional como sua fonte de dados.  
  
-   **AdventureWorksDW2012 ou posterior** -isso é um data warehouse relacional que é executado em uma instância do mecanismo de banco de dados. Ele fornece os dados originais usados pelos bancos de dados do Analysis Services e projetos que você criar e implantar em todo o tutorial. O tutorial presume que você está usando AdventureWorksDW2012, no entanto, fazer o trabalho de versões posteriores.
  
    Você pode usar esse banco de dados de exemplo com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores. Em geral, você deve usar a versão do banco de dados de exemplo correspondente à versão do mecanismo de banco de dados.
  
Para instalar o banco de dados, faça o seguinte:  
  
1.  Baixar uma [AdventureWorkDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) backup de banco de dados do GitHub.  
  
2.  Copie o arquivo de backup para o diretório de dados da instância do mecanismo de banco de dados do SQL Server local.
  
3.  Inicie o Microsoft SQL Server Management Studio e conecte-se à instância do Mecanismo do Banco de Dados.  
  
4.  Restaure o banco de dados.  
  
## <a name="step-4-grant-database-permissions"></a>Etapa 4: Conceder permissões de banco de dados  
As projetos de exemplo usam configurações de representação de fonte de dados que especificam o contexto de segurança sob o qual os dados são importados ou processados. Por padrão, as configurações de representação especificam a conta de serviço do Analysis Services para acessar os dados. Para usar essa configuração padrão, você deve garantir que a conta de serviço sob a qual o Analysis Services é executado tem permissões de leitor de dados o **AdventureWorksDW** banco de dados.  
  
> [!NOTE]  
> Para fins de aprendizagem, é recomendado usar a opção de representação de conta de serviço padrão e conceder permissões de leitura de dados à conta de serviço no SQL Server. Embora outras opções de representação estejam disponíveis, nem todas são adequadas para processar operações. Especificamente, a opção para usar as credenciais do usuário atual não tem suporte para processamento.  
  
1.  Determinar a conta de serviço. Você pode usar o SQL Server Configuration Manager ou o aplicativo de console de Serviços para exibir informações da conta. Se você instalou o Analysis Services como a instância padrão usando a conta padrão, o serviço será executado como **NT Service\MSSQLServerOLAPService**.  
  
2.  No Management Studio, conecte-se à instância do mecanismo do banco de dados.  
  
3.  Expanda a pasta Segurança, clique com o botão direito do mouse em Logons e selecione **Novo Logon**.  
  
4.  Na página Geral, em Nome de logon, digite **NT Service\MSSQLServerOLAPService** (ou qualquer conta na qual o serviço está sendo executado).  
  
5.  Clique em **Mapeamento de Usuário**.  
  
6.  Marque a caixa de seleção ao lado de **AdventureWorksDW** banco de dados. A associação de função deve incluir automaticamente **db_datareader** e **public**. Clique em **OK** para aceitar os padrões.  
  
## <a name="step-5-install-projects"></a>Etapa 5: Instalar projetos  

O tutorial inclui projetos de exemplo para que você possa comparar seus resultados em um projeto acabado ou iniciar uma lição que seja mais adiantada na sequência.  
  
1.  Baixe o [adventure-works-multidimensional-tutorial-projects.zip](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services) da Adventure Works para a página de exemplos do Analysis Services no GitHub.  
  
    Os projetos de tutorial funcionam para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores.  
  
2.  Mova o arquivo .zip para uma pasta debaixo da unidade de raiz (por exemplo, C:\Tutorial). Esta etapa mitigará o erro de "Caminho muito longo" que às vezes ocorre se você tentar descompactar os arquivos na pasta Downloads.  
  
3.  Descompacte os projetos de exemplo: clique com o botão direito do mouse no arquivo e selecione **Extrair Tudo**. Depois de extrair os arquivos, você deve ter pastas lição 1, 2, 3, 5, 6, 7, 8, 9, 10 concluída e o início da lição 4. 
  
4.  Remova as permissões somente leitura nesses arquivos. Clique com botão direito na pasta pai, selecione **propriedades**e desmarque a caixa de seleção **somente leitura**. Clique em **OK**. Aplique as alterações a essa pasta, subpastas e arquivos.  

5.  Abra o arquivo de solução (. sln) que corresponde à lição em que estão. Por exemplo, na pasta chamada "Lição 1 Concluída", abra o arquivo Analysis Services Tutorial.sln.  
  
6.  Implante a solução para verificar que permissões de banco de dados e informações de localização de servidor são configuradas corretamente.  
  
    Se o Analysis Services e o Mecanismo de Banco de Dados estiverem instalados como a instância padrão (MSSQLServer) e todo o software estiver sendo executado no mesmo computador, você poderá clicar em **Implantar Solução** no menu Criar para criar e implantar o projeto de exemplo na instância local do Analysis Services. Durante a implantação, dados são processados (ou importados) da **AdventureWorksDW** banco de dados na instância do mecanismo de banco de dados local. Um novo banco de dados do Analysis Services é criado na instância do Analysis Services que contém os dados recuperados do mecanismo de banco de dados.  
  
    Se você encontrar erros, analise as etapas anteriores sobre como configurar permissões de banco de dados. Além disso, talvez você precise alterar os nomes de servidores. O nome de servidor padrão é localhost. Se os servidores estiverem instalados em computadores remotos ou como instâncias nomeadas, substitua o padrão para usar um nome de servidor que seja válido para a instalação. Somado a isso, se os servidores estiverem em computadores remotos, talvez você precise configurar o Firewall do Windows para permitir o acesso a esses servidores.  
  
    O nome de servidor para conexão ao mecanismo de banco de dados é especificado no objeto Fonte de Dados da solução multidimensional (Tutorial do Adventure Works), visível no Gerenciador de Soluções.  
  
    O nome de servidor para conexão ao Analysis Services é especificado na guia Implantação de Páginas de Propriedades do projeto, também visível no Gerenciador de Soluções.  
  
7.  No SQL Server Management Studio, conecte-se ao Analysis Services. Verifique se o banco de dados nomeado **Tutorial do Analysis Services** está sendo executado no servidor.  
  
## <a name="next-step"></a>Próxima etapa  
Você agora está pronto para usar o tutorial. Para obter mais informações sobre como começar, consulte [Modelagem multidimensional &#40;Tutorial do Adventure Works&#41;](multidimensional-modeling-adventure-works-tutorial.md).  
  
## <a name="see-also"></a>Confira também  
[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  