---
title: Instalar dados de exemplo e projetos para o Tutorial de modelagem Multidimensional do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fc475b25-cbb2-408a-901f-9299299538c5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f0b4a69f7c1a6735fee26f1d622bc0f290e4677
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080394"
---
# <a name="install-sample-data-and-projects-for-the-analysis-services-multidimensional-modeling-tutorial"></a>Instalar dados de exemplo e projetos para o tutorial de modelagem multidimensional do Analysis Services
  Use as instruções e links fornecidos neste tópico para instalar todos os dados e arquivos de projeto usados nos Tutoriais do Analysis Services.  
  
## <a name="step-1-install-sql-server-software"></a>Etapa 1: Instalar o Software do SQL Server  
 As lições neste tutorial presumem que você tenha o seguinte software instalado. Todos os softwares a seguir são instalados usando a mídia de instalação do SQL Server. Para a simplicidade de implantação, você pode instalar todos os recursos em um único computador. Para instalar estes recursos, execute a Instalação do SQL Server e selecione-os na página Seleção de Recursos. Para obter mais informações, consulte [instalar o SQL Server 2014 do Assistente de instalação do &#40;instalação&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
-   Mecanismo de Banco de Dados  
  
-   Analysis Services  
  
     Analysis Services está disponível apenas nestas edições: Evaluation, Enterprise, Business Intelligence, Standard.  
  
     Observe que as edições do SQL Server Express não incluem o Analysis Services. [Baixe a edição Evaluation](https://go.microsoft.com/fwlink/?LinkId=392824) se desejar experimentar gratuitamente o software.  
  
     Por padrão, o Analysis Services é instalado como uma instância multidimensional, que você pode substituir escolhendo Modo de Servidor de Tabela na página de configuração do servidor do Assistente de Instalação. Se você desejar executar ambos os modos de servidor, reexecute a Instalação do SQL Server no mesmo computador para instalar uma segunda instância do Analysis Services no outro modo.  
  
-   SQL Server Management Studio  
  
 Como opção, instale o Excel para procurar seus dados multidimensionais à medida que você continua pelo tutorial. A instalação do Excel habilita o recurso **Analisar no Excel** que inicia o Excel usando uma lista de campo de Tabela Dinâmica que é conectada ao cubo que está sendo criado. Usar o Excel para procurar dados é recomendado porque você pode rapidamente criar um relatório dinâmico que permite interagir com os dados.  
  
 Como alternativa, você pode procurar dados usando o designer de consulta MDX interno que é embutido no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. O criador de consultas retorna os mesmos dados, menos os que são apresentados como um conjunto de linhas simples.  
  
## <a name="step-2-download-sql-server-data-tools---business-intelligence-for-visual-studio-2012"></a>Etapa 2: Baixar o SQL Server Data Tools - Business Intelligence para Visual Studio 2012  
 Nesta versão, o SQL Server Data Tools é baixado e instalado separadamente de outros recursos do SQL Server. Os designers e os modelos de projeto usados para criar modelos e relatórios de BI agora estão disponíveis como um download gratuito da Web.  
  
-   [Baixe a versão de Business Intelligence do SQL Server Data Tools](https://go.microsoft.com/fwlink/p/?LinkID=322038). O arquivo é salvo na pasta de Downloads. Execute a instalação para instalar a ferramenta.  
  
     Reinicialize o computador para concluir a instalação.  
  
## <a name="step-3-install-databases"></a>Etapa 3: Instalar bancos de dados  
 Um modelo multidimensional do Analysis Services usa dados transacionais que você importa de um RDBMS. Para este tutorial, você usará o banco de dados relacional a seguir como sua fonte de dados.  
  
-   **AdventureWorksDW2012** -isso é um data warehouse relacional que é executado em uma instância do mecanismo de banco de dados. Ele fornece os dados originais que serão usados pelos bancos de dados do Analysis Services e projetos que você criar e implantar ao longo do tutorial.  
  
     Você pode usar esse banco de dados de exemplo com o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] assim como o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
 Para instalar este banco de dados, execute o seguinte procedimento:  
  
1.  Baixe o banco de dados [AdventureWorkDW2012](https://go.microsoft.com/fwlink/p/?LinkID=221770) na página de amostras do produto no CodePlex.  
  
     O nome de arquivo do banco de dados é AdvntureWorksDW2012_Data.mdf. O arquivo deve estar na pasta Downloads em seu computador.  
  
2.  Copie o arquivo AdventureWorksDW2012_Data.mdf para o diretório de dados da instância do Mecanismo de Banco de Dados do SQL Server local. Por padrão, ele está localizado em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data.  
  
3.  Inicie o Microsoft SQL Server Management Studio e conecte-se à instância do Mecanismo do Banco de Dados.  
  
4.  Clique com o botão direito do mouse em Bancos de dados e clique em **Anexar**.  
  
5.  Clique em **Adicionar**.  
  
6.  Selecione o arquivo de banco de dados **AdventureWorksDW2012_Data.mdf** e clique em **OK**. Se o arquivo não estiver listado, verifique a pasta C:\Arquivos de Programas\MSSQL12.MSSQLSERVER\MSSQL\Data para ver se ele está lá.  
  
7.  Em detalhes de banco de dados, remova a entrada de arquivo de log. O programa de instalação pressupõe que você tem um arquivo de log, mas não há arquivo de log no exemplo. Um novo arquivo de log será criado automaticamente quando você anexar o banco de dados. Selecione o arquivo de log, clique em **Remover**e em **OK** para anexar somente o arquivo do banco de dados primário.  
  
## <a name="step-4-grant-database-permissions"></a>Etapa 4: Permissões Grant de banco de dados  
 As projetos de exemplo usam configurações de representação de fonte de dados que especificam o contexto de segurança sob o qual os dados são importados ou processados. Por padrão, as configurações de representação especificam a conta de serviço do Analysis Services para acessar os dados. Para usar essa configuração padrão, você deve assegurar que a conta de serviço na qual o Analysis Services é executado tem permissões de leitura de dados no banco de dados **AdventureWorksDW2012** .  
  
> [!NOTE]  
>  Para fins de aprendizagem, é recomendado usar a opção de representação de conta de serviço padrão e conceder permissões de leitura de dados à conta de serviço no SQL Server. Embora outras opções de representação estejam disponíveis, nem todas são adequadas para processar operações. Especificamente, a opção para usar as credenciais do usuário atual não tem suporte para processamento.  
  
1.  Determinar a conta de serviço. Você pode usar o SQL Server Configuration Manager ou o aplicativo de console de Serviços para exibir informações da conta. Se você instalou o Analysis Services como a instância padrão usando a conta padrão, o serviço será executado como **NT Service\MSSQLServerOLAPService**.  
  
2.  No Management Studio, conecte-se à instância do mecanismo do banco de dados.  
  
3.  Expanda a pasta Segurança, clique com o botão direito do mouse em Logons e selecione **Novo Logon**.  
  
4.  Na página Geral, em Nome de logon, digite **NT Service\MSSQLServerOLAPService** (ou qualquer conta na qual o serviço está sendo executado).  
  
5.  Clique em **Mapeamento de Usuário**.  
  
6.  Marque a caixa de seleção ao lado do banco de dados **AdventureWorksDW2012** . A associação de função deve incluir automaticamente **db_datareader** e **public**. Clique em **OK** para aceitar os padrões.  
  
## <a name="step-5-install-projects"></a>Etapa 5: Instalar projetos  
 O tutorial inclui projetos de exemplo para que você possa comparar seus resultados em um projeto acabado ou iniciar uma lição que seja mais adiantada na sequência.  
  
 O arquivo de projeto para a Lição 4 é particularmente importante porque fornece a base não somente para essa lição, mas todas as lições subsequentes. Em contraste com os arquivos de projeto anteriores, onde as etapas no tutorial resultam em uma cópia exata dos arquivos de projeto concluídos, o projeto de exemplo da Lição 4 inclui novas informações de modelo que não estão localizadas no modelo que você criou nas lições 1 a 3. A Lição 4 presume que você esteja iniciando com um arquivo de projeto de exemplo que está disponível no download a seguir.  
  
1.  Baixe o [Tutorial do Analysis Services do SQL Server 2012](https://go.microsoft.com/fwlink/p/?LinkID=221866) na página de amostras do produto no CodePlex.  
  
     Os tutoriais do 2012 são válidos para a versão do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] .  
  
     O arquivo "Analysis Services Tutorial SQL Server 2012.zip" será ser salvo na pasta Downloads em seu computador.  
  
2.  Mova o arquivo .zip para uma pasta debaixo da unidade de raiz (por exemplo, C:\Tutorial). Esta etapa mitigará o erro de "Caminho muito longo" que às vezes ocorre se você tentar descompactar os arquivos na pasta Downloads.  
  
3.  Descompacte os projetos de exemplo: clique com o botão direito do mouse no arquivo e selecione **Extrair Tudo**. Depois de extrair os arquivos, você deve ter os seguintes projetos instalados em seu computador:  
  
    -   Lição 1 concluída  
  
    -   Lição 2 concluída  
  
    -   Lição 3 concluída  
  
    -   Lição 4 concluída  
  
    -   Lesson 4 Iniciar  
  
    -   Lição 5 concluída  
  
    -   Lição 6 concluída  
  
    -   Lição 7 concluída  
  
    -   Lição 8 concluída  
  
    -   Lição 9 concluída  
  
    -   Lição 10 concluída  
  
4.  Remova as permissões somente leitura nesses arquivos. Clique com o botão direito do mouse na pasta pai, “Tutorial do SQL Server Analysis Services 2012”, selecione **Propriedades**e desmarque a caixa de seleção **Somente leitura**. Clique em **OK**. Aplique as alterações a essa pasta, subpastas e arquivos.  
  
5.  Inicie o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
6.  Abra o arquivo de solução (.sln) que corresponde à lição você está usando. Por exemplo, na pasta chamada "Lição 1 Concluída", abra o arquivo Analysis Services Tutorial.sln.  
  
7.  Implante a solução para verificar se as permissões de banco de dados e informações de local de servidor estão configuradas corretamente.  
  
     Se o Analysis Services e o Mecanismo de Banco de Dados estiverem instalados como a instância padrão (MSSQLServer) e todo o software estiver sendo executado no mesmo computador, você poderá clicar em **Implantar Solução** no menu Criar para criar e implantar o projeto de exemplo na instância local do Analysis Services. Durante a implantação, os dados serão processados (ou importados) do banco de dados **AdventureWorksDW2012** na instância do Mecanismo de Banco de Dados local. Um novo banco de dados do Analysis Services será criado na instância do Analysis Services que contém os dados recuperados do Mecanismo de Banco de Dados.  
  
     Se você encontrar erros, analise as etapas anteriores sobre como configurar permissões de banco de dados. Além disso, talvez você precise alterar os nomes de servidores. O nome de servidor padrão é localhost. Se os servidores estiverem instalados em computadores remotos ou como instâncias nomeadas, substitua o padrão para usar um nome de servidor que seja válido para a instalação. Somado a isso, se os servidores estiverem em computadores remotos, talvez você precise configurar o Firewall do Windows para permitir o acesso a esses servidores.  
  
     O nome de servidor para conexão ao mecanismo de banco de dados é especificado no objeto Fonte de Dados da solução multidimensional (Tutorial do Adventure Works), visível no Gerenciador de Soluções.  
  
     O nome de servidor para conexão ao Analysis Services é especificado na guia Implantação de Páginas de Propriedades do projeto, também visível no Gerenciador de Soluções.  
  
8.  Inicie o SQL Server Management Studio. No SQL Server Management Studio, conecte-se ao Analysis Services. Verifique se um banco de dados nomeado **Tutorial do Analysis Services** está sendo executado no servidor.  
  
## <a name="next-step"></a>Próxima etapa  
 Você agora está pronto para usar o tutorial. Para obter mais informações sobre como começar, consulte [Modelagem multidimensional &#40;Tutorial do Adventure Works&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o SQL Server 2014 do Assistente de instalação &#40;programa de instalação&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [Configure the Windows Firewall to Allow Analysis Services Access](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)   
 [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
