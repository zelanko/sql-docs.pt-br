---
title: Instalar Analysis Services projetos e dados de exemplo | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c89ee3edf9338c4f74b0738d930ee74dbec7244
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794983"
---
# <a name="install-sample-data-and-multidimensional-projects"></a>Instalar dados de exemplo e projetos multidimensionais 
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

Use as instruções e os links fornecidos neste artigo para instalar os dados e os arquivos de projeto usados nos tutoriais de Analysis Services. 
  
## <a name="step-1-install-prerequisites"></a>Etapa 1: Instalar pré-requisitos 
As lições neste tutorial presumem que você tenha o seguinte software instalado. Você pode instalar todos os recursos em um único computador. Para instalar estes recursos, execute a Instalação do SQL Server e selecione-os na página Seleção de Recursos.  
  
-   Mecanismo de Banco de Dados do SQL Server  
  
-   SQL Server Analysis Services  (SSAS) 
  
    Analysis Services está disponível somente nestas edições: Avaliação, Enterprise, Business Intelligence, Standard. Não há suporte para modelos multidimensionais no Azure Analysis Services.
  
    Por padrão, o Analysis Services 2016 e posterior é instalado como uma instância tabular, que pode ser substituída escolhendo o modo de servidor multidimensional na página configuração do servidor do assistente de instalação.
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>Etapa 2: Baixe e instale ferramentas de desenvolvedor e gerenciamento
O SQL Server Data Tools (SSDT) para Visual Studio é baixado e instalado separadamente de outros recursos do SQL Server. Os designers e modelos de projeto usados para criar modelos de BI e relatórios estão incluídos no SSDT para Visual Studio 2015 ou como [pacotes NuGet](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) para o visual Studio 2017.  
  
[Baixar o SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542).   

O SQL Server Management Studio (SSMS) é baixado e instalado separadamente de outros recursos do SQL Server.  

[Baixar o SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)  

Como opção, instale o Excel para procurar seus dados multidimensionais à medida que você continua pelo tutorial. A instalação do Excel habilita o recurso **Analisar no Excel** que inicia o Excel usando uma lista de campo de Tabela Dinâmica que é conectada ao cubo que está sendo criado. Usar o Excel para procurar dados é recomendado porque você pode rapidamente criar um relatório dinâmico que permite interagir com os dados.  
  
Como alternativa, você pode procurar dados usando o designer de consulta MDX interno que é embutido no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. O criador de consultas retorna os mesmos dados, menos os que são apresentados como um conjunto de linhas simples.  
  
## <a name="step-3-install-databases"></a>Etapa 3: Instalar bancos de dados  
Um modelo multidimensional do Analysis Services usa dados transacionais que você importa de um RDBMS. Para os fins deste tutorial, você usará o banco de dados relacional a seguir como sua fonte.  
  
-   **AdventureWorksDW2012 ou posterior** – este é um data warehouse relacional que é executado em uma instância de mecanismo de banco de dados. Ele fornece os dados originais usados pelo Analysis Services bancos de dados e projetos que você cria e implanta em todo o tutorial. O tutorial pressupõe que você esteja usando AdventureWorksDW2012, no entanto, as versões posteriores funcionam.
  
    Você pode usar este banco de dados [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] de exemplo com o e posterior. Em geral, você deve usar a versão do banco de dados de exemplo correspondente à versão do mecanismo de banco de dados.
  
Para instalar o banco de dados, faça o seguinte:  
  
1.  Baixe um backup de banco de dados [AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) do github.  
  
2.  Copie o arquivo de backup para o diretório de dados da instância de Mecanismo de Banco de Dados de SQL Server local.
  
3.  Inicie o Microsoft SQL Server Management Studio e conecte-se à instância do Mecanismo do Banco de Dados.  
  
4.  Restaure o banco de dados.  
  
## <a name="step-4-grant-database-permissions"></a>Etapa 4: Conceder permissões de banco de dados  
As projetos de exemplo usam configurações de representação de fonte de dados que especificam o contexto de segurança sob o qual os dados são importados ou processados. Por padrão, as configurações de representação especificam a conta de serviço do Analysis Services para acessar os dados. Para usar essa configuração padrão, você deve garantir que a conta de serviço na qual Analysis Services é executado tenha permissões de leitor de dados no banco de dados **AdventureWorksDW** .  
  
> [!NOTE]  
> Para fins de aprendizagem, é recomendado usar a opção de representação de conta de serviço padrão e conceder permissões de leitura de dados à conta de serviço no SQL Server. Embora outras opções de representação estejam disponíveis, nem todas são adequadas para processar operações. Especificamente, a opção para usar as credenciais do usuário atual não tem suporte para processamento.  
  
1.  Determinar a conta de serviço. Você pode usar o SQL Server Configuration Manager ou o aplicativo de console de Serviços para exibir informações da conta. Se você instalou o Analysis Services como a instância padrão usando a conta padrão, o serviço será executado como **NT Service\MSSQLServerOLAPService**.  
  
2.  No Management Studio, conecte-se à instância do mecanismo do banco de dados.  
  
3.  Expanda a pasta Segurança, clique com o botão direito do mouse em Logons e selecione **Novo Logon**.  
  
4.  Na página Geral, em Nome de logon, digite **NT Service\MSSQLServerOLAPService** (ou qualquer conta na qual o serviço está sendo executado).  
  
5.  Clique em **Mapeamento de Usuário**.  
  
6.  Marque a caixa de seleção ao lado do banco de dados **AdventureWorksDW** . A associação de função deve incluir automaticamente **db_datareader** e **public**. Clique em **OK** para aceitar os padrões.  
  
## <a name="step-5-install-projects"></a>Etapa 5: Instalar projetos  

O tutorial inclui projetos de exemplo para que você possa comparar seus resultados em um projeto acabado ou iniciar uma lição que seja mais adiantada na sequência.  
  
1.  Baixe o [Adventure-Works-multidimensional-tutorial-Projects. zip](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services) da página de exemplos da Adventure Works for Analysis Services no github.  
  
    Os projetos do tutorial funcionam [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para o e posterior.  
  
2.  Mova o arquivo .zip para uma pasta debaixo da unidade de raiz (por exemplo, C:\Tutorial). Essa etapa reduz o erro de "caminho muito longo" que às vezes ocorre se você tentar descompactar os arquivos na pasta de downloads.  
  
3.  Descompacte os projetos de exemplo: clique com o botão direito do mouse no arquivo e selecione **Extrair Tudo**. Depois de extrair os arquivos, você deve ter as pastas lição 1, 2, 3, 5, 6, 7, 8, 9, 10 concluídos e a lição 4 começar. 
  
4.  Remova as permissões somente leitura nesses arquivos. Clique com o botão direito do mouse na pasta pai, selecione **Propriedades**e desmarque a caixa de seleção **somente leitura**. Clique em **OK**. Aplique as alterações a essa pasta, subpastas e arquivos.  

5.  Abra o arquivo da solução (. sln) que corresponde à lição em que você está. Por exemplo, na pasta chamada "Lição 1 Concluída", abra o arquivo Analysis Services Tutorial.sln.  
  
6.  Implante a solução para verificar se as permissões de banco de dados e as informações de local do servidor estão configuradas corretamente.  
  
    Se o Analysis Services e o Mecanismo de Banco de Dados estiverem instalados como a instância padrão (MSSQLServer) e todo o software estiver sendo executado no mesmo computador, você poderá clicar em **Implantar Solução** no menu Criar para criar e implantar o projeto de exemplo na instância local do Analysis Services. Durante a implantação, os dados são processados (ou importados) do banco de dados **AdventureWorksDW** na instância de mecanismo de banco de dados local. Um novo banco de dados de Analysis Services é criado na instância de Analysis Services que contém o dado recuperado do Mecanismo de Banco de Dados.  
  
    Se você encontrar erros, analise as etapas anteriores sobre como configurar permissões de banco de dados. Além disso, talvez você precise alterar os nomes de servidores. O nome de servidor padrão é localhost. Se os servidores estiverem instalados em computadores remotos ou como instâncias nomeadas, substitua o padrão para usar um nome de servidor que seja válido para a instalação. Somado a isso, se os servidores estiverem em computadores remotos, talvez você precise configurar o Firewall do Windows para permitir o acesso a esses servidores.  
  
    O nome de servidor para conexão ao mecanismo de banco de dados é especificado no objeto Fonte de Dados da solução multidimensional (Tutorial do Adventure Works), visível no Gerenciador de Soluções.  
  
    O nome de servidor para conexão ao Analysis Services é especificado na guia Implantação de Páginas de Propriedades do projeto, também visível no Gerenciador de Soluções.  
  
7.  No SQL Server Management Studio, conecte-se ao Analysis Services. Verifique se o banco de dados nomeado **Tutorial do Analysis Services** está sendo executado no servidor.  
  
## <a name="next-step"></a>Próxima etapa  
Você agora está pronto para usar o tutorial. Para obter mais informações sobre como começar, consulte [Modelagem multidimensional &#40;Tutorial do Adventure Works&#41;](multidimensional-modeling-adventure-works-tutorial.md).  
  
## <a name="see-also"></a>Confira também  
[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
