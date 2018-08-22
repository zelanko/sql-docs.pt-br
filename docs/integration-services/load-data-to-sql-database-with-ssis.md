---
title: Carregar dados no Banco de Dados SQL do Azure com o SSIS (SQL Server Integration Services) | Microsoft Docs
description: Mostra como criar um pacote do SSIS (SQL Server Integration Services) para mover dados de uma ampla variedade de fontes de dados para o Banco de Dados SQL do Azure.
documentationcenter: NA
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.technology: integration-services
ms.devlang: NA
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.custom: loading
ms.date: 08/14/2018
ms.author: douglasl
author: douglaslMS
manager: craigg-msft
ms.openlocfilehash: ed87e5a83e992ba5de6289d72465d92c94126748
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40175015"
---
# <a name="load-data-into-azure-sql-database-with-sql-server-integration-services-ssis"></a>Carregar dados no Banco de Dados SQL do Azure com o SSIS (SQL Server Integration Services)

Crie um pacote do SSIS (SQL Server Integration Services) para carregar dados no [Banco de Dados SQL do Azure](/azure/sql-database/). Opcionalmente, você pode reestruturar, transformar e limpar os dados conforme eles passam pelo fluxo de dados do SSIS.

Este artigo mostra como fazer o seguinte:

* Criar um projeto do Integration Services no Visual Studio.
* Criar um pacote do SSIS que carrega dados da fonte para o destino.
* Executar o pacote do SSIS para carregar os dados.

## <a name="basic-concepts"></a>Conceitos básicos

O pacote é a unidade básica de trabalho no SSIS. Os pacotes relacionados são agrupados em projetos. Você cria projetos e elabora pacotes no Visual Studio com o SQL Server Data Tools. O processo de design é um processo visual em que você arrasta e solta componentes da Caixa de ferramentas na superfície de design, conecta-os e define as respectivas propriedades. Depois de concluir seu pacote, você poderá executá-lo e, opcionalmente, implantá-lo no SQL Server ou no Banco de Dados SQL para realizar gerenciamento, monitoramento e segurança abrangentes.

Uma introdução detalhada ao SSIS está além do escopo deste artigo. Para saber mais, leia os seguintes artigos:

- [SQL Server Integration Services](sql-server-integration-services.md)

- [Como criar um pacote ETL](ssis-how-to-create-an-etl-package.md)

## <a name="about-the-solution"></a>Sobre a solução

A solução é um pacote típico que usa uma tarefa de fluxo de dados que contém uma fonte e um destino. Essa abordagem permite uma ampla variedade de fontes de dados, incluindo o SQL Server e o Banco de Dados SQL do Azure.

Este tutorial usa o SQL Server como fonte de dados. O SQL Server é executado localmente ou em uma máquina virtual do Azure.

Para conectar-se ao SQL Server e ao Banco de Dados SQL, você pode usar um gerenciador de conexões ADO.NET com uma fonte e um destino ou um gerenciador de conexões OLE DB com uma fonte e um destino. Este tutorial usa o ADO.NET porque ele tem menos opções de configuração. O OLE DB pode resultar em um desempenho ligeiramente melhor do que o ADO.NET.

Como atalho, é possível usar o Assistente de Importação e Exportação do SQL Server para criar o pacote básico. Em seguida, salve o pacote e abra-o no Visual Studio ou no SSDT para exibi-lo e personalizá-lo. Para obter mais informações, consulte [Importar e exportar dados com o Assistente para Importação e Exportação do SQL Server](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

## <a name="prerequisites"></a>Prerequisites
Para realizar este tutorial, você precisa do seguinte:

1. **Do SSIS (SQL Server Integration Services)**. O SSIS é um componente do SQL Server e requer uma versão licenciada, ou uma versão de avaliação ou do desenvolvedor, do SQL Server. Para obter uma versão de avaliação do SQL Server, consulte [Avaliar SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm).
2. **Visual Studio** (opcional). Para obter o Visual Studio Community Edition gratuito, veja [Visual Studio Community][Visual Studio Community]. Se não quiser instalar o Visual Studio, você poderá instalar apenas o SSDT (SQL Server Data Tools). O SSDT instala uma versão do Visual Studio com funcionalidade limitada.
3. **Do SSDT (SQL Server Data Tools) para Visual Studio**. Para obter o SQL Server Data Tools para Visual Studio, veja [Baixar o SSDT (SQL Server Data Tools)][Download SQL Server Data Tools (SSDT)].
4. **Um banco de dados do Banco de Dados SQL do Azure e as permissões**. Este tutorial mostra como se conectar a uma instância do Banco de Dados SQL e carregar dados nela. Você precisa das permissões para se conectar, criar uma tabela e carregar dados.
5. **De dados de exemplo**. Este tutorial usa dados de exemplo armazenados no SQL Server, no banco de dados de exemplo AdventureWorks, como os dados de origem a serem carregados no Banco de Dados SQL. Para obter o banco de dados de exemplo AdventureWorks, confira [Bancos de dados de exemplo AdventureWorks][AdventureWorks 2014 Sample Databases].
6. **De uma regra de firewall**. Você precisa criar uma regra de firewall no Banco de Dados SQL com o endereço IP do computador local antes de carregar dados no Banco de Dados SQL.

## <a name="create-a-new-integration-services-project"></a>Criar um novo projeto do Integration Services
1. Inicie o Visual Studio.
2. No menu **Arquivo**, selecione **Novo | Projeto**.
3. Navegue até os tipos de projeto **Instalados | Modelos | Business Intelligence | Integration Services**.
4. Selecione **Projeto do Integration Services**. Forneça valores de **Nome** e **Localização** e, em seguida, selecione **OK**.

O Visual Studio é aberto e cria um projeto do SSIS (Integration Services). Em seguida, o Visual Studio abre o designer do único novo pacote do SSIS (Package.dtsx) no projeto. Você verá as seguintes áreas na tela:

* À esquerda, a **Caixa de ferramentas** dos componentes do SSIS.
* No meio, a superfície de design, com várias guias. Geralmente, você usa pelo menos as guias **Fluxo de Controle** e **Fluxo de Dados**.
* À direita, os painéis **Gerenciador de Soluções** e **Propriedades**.
  
    ![][01]

## <a name="create-the-basic-data-flow"></a>Criar o fluxo de dados básico
1. Arraste uma Tarefa Fluxo de Dados da Caixa de ferramentas até o centro da superfície de design (na guia **Fluxo de Controle**).
   
    ![][02]
2. Clique duas vezes na Tarefa Fluxo de Dados para mudar para a guia Fluxo de Dados.
3. Na lista Outras Fontes, da Caixa de ferramentas, arraste uma Fonte do ADO.NET até a superfície de design. Mantendo o adaptador de fonte selecionado, altere o nome dele para **fonte do SQL Server** no painel **Propriedades**.
4. Na lista Outros Destinos, na Caixa de ferramentas, arraste um Destino do ADO.NET até a superfície de design, na fonte do ADO.NET. Mantendo o adaptador de destino selecionado, altere seu nome para **Destino do BD SQL** no painel **Propriedades**.
   
    ![][09]

## <a name="configure-the-source-adapter"></a>Configurar o adaptador de fonte
1. Clique duas vezes no adaptador de fonte para abrir o **Editor de Origem ADO.NET**.
   
    ![][03]
2. Na guia **Gerenciador de Conexões** do **Editor de Origem ADO.NET**, clique no botão **Novo** próximo à lista do **Gerenciador de conexões do ADO.NET** para abrir a caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET** e criar configurações de conexão para o banco de dados do SQL Server do qual este tutorial carrega os dados.
   
    ![][04]
3. Na caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET**, clique no botão **Novo** para abrir a caixa de diálogo **Gerenciador de Conexões** e criar uma conexão de dados.
   
    ![][05]
4. Na caixa de diálogo **Gerenciador de Conexões**, faça o seguinte.
   
   1. Para **Provedor**, selecione o Provedor de Dados SqlClient.
   2. Para **Nome do servidor**, digite o nome do SQL Server.
   3. Na seção **Fazer logon no servidor**, selecione ou insira as informações de autenticação.
   4. Na seção **Conectar a um banco de dados**, selecione o banco de dados de exemplo AdventureWorks.
   5. Clique em **Testar Conexão**.
      
       ![][06]
   6. Na caixa de diálogo que relata os resultados do teste de conexão, clique em **OK** para retornar para a caixa de diálogo **Gerenciador de Conexões**.
   7. Na caixa de diálogo **Gerenciador de Conexões**, clique em **OK** para retornar para a caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET**.
5. Na caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET**, clique em **OK** para retornar para o **Editor de Origem ADO.NET**.
6. No **Editor de Origem ADO.NET**, na lista **Nome da tabela ou da exibição**, selecione a tabela **Sales.SalesOrderDetail**.
   
    ![][07]
7. Clique em **Visualização** para ver as primeiras 200 linhas de dados da tabela de origem na caixa de diálogo **Visualizar Resultados da Consulta**.
   
    ![][08]
8. Na caixa de diálogo **Visualizar Resultados da Consulta**, clique em **Fechar** para retornar para o **Editor de Origem ADO.NET**.
9. No **Editor de Origem ADO.NET**, clique em **OK** terminar a configuração da fonte de dados.

## <a name="connect-the-source-adapter-to-the-destination-adapter"></a>Conectar o adaptador de fonte ao adaptador de destino
1. Selecione o adaptador de fonte na superfície de design.
2. Selecione a seta azul que se estende do adaptador de fonte e arraste-a até o editor de destino até que ela se encaixe.
   
    ![][10]
   
    Em um pacote do SSIS típico, você pode usar uma variedade de componentes adicionais da Caixa de ferramentas do SSIS entre a fonte e o destino para reestruturar, transformar e limpar seus dados, conforme eles passam pelo fluxo de dados do SSIS. Para deixar este exemplo o mais simples possível, estamos conectando a fonte diretamente com o destino.

## <a name="configure-the-destination-adapter"></a>Configurar o adaptador de destino
1. Clique duas vezes no adaptador de destino para abrir o **Editor de Destino ADO.NET**.
   
    ![][11]
2. Na guia **Gerenciador de Conexões** do **Editor de Destino ADO.NET**, clique no botão **Novo** próximo à lista do **Gerenciador de conexões** para abrir a caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET** e criar configurações de conexão para o banco de dados do Banco de Dados SQL do Azure, no qual este tutorial carrega dados.
3. Na caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET**, clique no botão **Novo** para abrir a caixa de diálogo **Gerenciador de Conexões** e criar uma conexão de dados.
4. Na caixa de diálogo **Gerenciador de Conexões**, faça o seguinte.
   1. Para **Provedor**, selecione o Provedor de Dados SqlClient.
   2. Para **Nome do servidor**, insira o nome do Banco de Dados SQL.
   3. Na seção **Fazer logon no servidor**, selecione **Usar autenticação do SQL Server** e insira as informações de autenticação.
   4. Na seção **Conectar a um banco de dados**, selecione um banco de dados do Banco de Dados SQL existente.
   5. Clique em **Testar Conexão**.
   6. Na caixa de diálogo que relata os resultados do teste de conexão, clique em **OK** para retornar para a caixa de diálogo **Gerenciador de Conexões**.
   7. Na caixa de diálogo **Gerenciador de Conexões**, clique em **OK** para retornar para a caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET**.
5. Na caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET**, clique em **OK** para retornar para o **Editor de Destino ADO.NET**.
6. No **Editor de Destino ADO.NET**, clique em **Novo**, ao lado da lista **Usar uma tabela ou exibição**, para abrir a caixa de diálogo **Criar Tabela** e criar uma tabela de destino com uma lista de colunas que corresponda à tabela de origem.
   
    ![][12a]
7. Na caixa de diálogo **Criar Tabela**, faça o seguinte.
   
   1. Altere o nome da tabela de destino para **SalesOrderDetail**.
      
       ![][12b]

   2. Clique em **OK** para criar a tabela e retornar ao **Editor de Destino ADO.NET**.
8. No **Editor de Destino ADO.NET**, selecione a guia **Mapeamentos** para ver como as colunas da fonte são mapeadas para as colunas do destino.
   
    ![][13]
9. Clique em **OK** para concluir a configuração do destino.

## <a name="run-the-package-to-load-the-data"></a>Executar o pacote para carregar os dados
Execute o pacote clicando no botão **Iniciar** na barra de ferramentas ou selecionando uma das opções **Executar** do menu **Depurar**.

Os parágrafos a seguir descrevem o que você vê ao criar o pacote com a segunda opção descrita neste artigo, ou seja, com um fluxo de dados que contém uma origem e um destino.

Conforme o pacote começar a executar, você verá rodas amarelas giratórias indicando a atividade, bem como o número de linhas processadas até aquele momento.

![][14]

Quando a execução do pacote for concluída, você verá marcas de seleção verdes para indicar êxito, bem como o número total de linhas de dados carregados da fonte para o destino.

![][15]

Parabéns! Você conseguiu usar o SQL Server Integration Services para carregar dados no Banco de Dados SQL do Azure.

## <a name="next-steps"></a>Próximas etapas

- Saiba como depurar e solucionar problemas de pacotes diretamente no ambiente de design. Comece aqui: [Ferramentas de solução de problemas para desenvolvimento de pacotes][Troubleshooting Tools for Package Development].

- Saiba como implantar seus pacotes e projetos do SSIS no servidor do Integration Services ou em outro local de armazenamento. Comece aqui: [Implantação de projetos e pacotes][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/load-data-to-sql-database-with-ssis/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-database-with-ssis/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-database-with-ssis/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-database-with-ssis/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-database-with-ssis/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-database-with-ssis/test-connection-06.png
[07]:  ./media/load-data-to-sql-database-with-ssis/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-database-with-ssis/preview-data-08.png
[09]:  ./media/load-data-to-sql-database-with-ssis/source-destination-09.png
[10]:  ./media/load-data-to-sql-database-with-ssis/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-database-with-ssis/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-database-with-ssis/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-database-with-ssis/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-database-with-ssis/column-mapping-13.png
[14]:  ./media/load-data-to-sql-database-with-ssis/package-running-14.png
[15]:  ./media/load-data-to-sql-database-with-ssis/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]: https://www.microsoft.com/download/details.aspx?id=54798
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2017
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
