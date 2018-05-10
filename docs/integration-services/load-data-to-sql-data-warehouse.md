---
title: Carregar dados do SQL Server no SQL Data Warehouse do Azure (SSIS) | Microsoft Docs
description: Mostra como criar um pacote do SSIS (SQL Server Integration Services) para mover dados de uma ampla variedade de fontes de dados para o SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: douglaslMS
manager: craigg-msft
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.custom: loading
ms.date: 04/04/2018
ms.author: douglasl
ms.openlocfilehash: e627fdad03bf3159a0ed9c730381fde53c86ee9f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="load-data-from-sql-server-to-azure-sql-data-warehouse-with-sql-server-integration-services-ssis"></a>Carregar dados do SQL Server no SQL Data Warehouse do Azure com o SSIS (SQL Server Integration Services)

Crie um pacote do SSIS (SQL Server Integration Services) para carregar dados do SQL Server no [SQL Data Warehouse do Azure](/azure/sql-data-warehouse/index.md). Opcionalmente, você pode reestruturar, transformar e limpar os dados conforme eles passam pelo fluxo de dados do SSIS.

Neste tutorial, você vai:

* Criar um projeto do Integration Services no Visual Studio.
* Conectar-se a fontes de dados, incluindo o SQL Server (como uma fonte) e SQL Data Warehouse (como um destino).
* Criar um pacote do SSIS que carrega dados da fonte para o destino.
* Executar o pacote do SSIS para carregar os dados.

Este tutorial usa o SQL Server como fonte de dados. O SQL Server pode estar em execução localmente ou em uma máquina virtual do Azure.

## <a name="basic-concepts"></a>Conceitos básicos
O pacote é a unidade de trabalho no SSIS. Os pacotes relacionados são agrupados em projetos. Você cria projetos e elabora pacotes no Visual Studio com o SQL Server Data Tools. O processo de design é um processo visual em que você arrasta e solta componentes da Caixa de ferramentas na superfície de design, conecta-os e define as respectivas propriedades. Depois de concluir o pacote, você pode, opcionalmente, implantá-lo no SQL Server para um gerenciamento, monitoramento e uma segurança mais abrangentes.

## <a name="options-for-loading-data-with-ssis"></a>Opções de carregamento de dados com o SSIS
O SSIS (SQL Server Integration Services) é um conjunto flexível de ferramentas que oferece uma variedade de opções para se conectar ao SQL Data Warehouse e carregar dados nele.

1. Use um Destino do ADO NET para conectar-se ao SQL Data Warehouse. Este tutorial usa um Destino do ADO NET porque ele tem menos opções de configuração.
2. Use um Destino do OLE DB para conectar-se ao SQL Data Warehouse. Esta opção pode resultar em um desempenho ligeiramente melhor do que o Destino do ADO NET.
3. Use a Tarefa de upload de Blobs do Azure para preparar os dados no Armazenamento de Blobs do Azure. Depois, use a tarefa Executar SQL do SSIS para iniciar um script do PolyBase que carrega os dados no SQL Data Warehouse. Essa opção proporciona o melhor desempenho dentre as três opções listadas. Para obter a Tarefa de upload de Blobs do Azure, baixe o [Microsoft SQL Server 2016 Integration Services Feature Pack para Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. Para saber mais sobre o PolyBase, veja o [Guia do PolyBase][PolyBase Guide].

## <a name="before-you-start"></a>Antes de iniciar
Para realizar este tutorial, você precisa:

1. **Do SSIS (SQL Server Integration Services)**. O SSIS é um componente do SQL Server e requer uma versão de avaliação ou uma versão licenciada do SQL Server. Para obter uma versão de avaliação do SQL Server 2016 Preview, veja [Avaliações do SQL Server][SQL Server Evaluations].
2. **Do Visual Studio**. Para obter o Visual Studio Community Edition gratuito, veja [Visual Studio Community][Visual Studio Community].
3. **Do SSDT (SQL Server Data Tools) para Visual Studio**. Para obter o SQL Server Data Tools para Visual Studio, veja [Baixar o SSDT (SQL Server Data Tools)][Download SQL Server Data Tools (SSDT)].
4. **De dados de exemplo**. Este tutorial usa dados de exemplo armazenados no SQL Server, no banco de dados de exemplo AdventureWorks, como os dados de origem a serem carregados no SQL Data Warehouse. Para obter o banco de dados de exemplo AdventureWorks, veja [Bancos de dados de exemplo AdventureWorks 2014][AdventureWorks 2014 Sample Databases].
5. **De um banco de dados do SQL Data Warehouse e as respectivas permissões**. Este tutorial se conecta a uma instância do SQL Data Warehouse e carrega dados nela. Você precisa das permissões para criar uma tabela e carregar dados.
6. **De uma regra de firewall**. Você precisa criar uma regra de firewall no SQL Data Warehouse com o endereço IP do seu computador local antes de carregar dados no SQL Data Warehouse.

## <a name="step-1-create-a-new-integration-services-project"></a>Etapa 1: criar um projeto do Integration Services
1. Inicie o Visual Studio.
2. No menu **Arquivo**, selecione **Novo | Projeto**.
3. Navegue até os tipos de projeto **Instalados | Modelos | Business Intelligence | Integration Services**.
4. Selecione **Projeto do Integration Services**. Forneça valores de **Nome** e **Localização** e, em seguida, selecione **OK**.

O Visual Studio é aberto e cria um projeto do SSIS (Integration Services). Em seguida, o Visual Studio abre o designer do único novo pacote do SSIS (Package.dtsx) no projeto. Você verá as seguintes áreas na tela:

* À esquerda, a **Caixa de ferramentas** dos componentes do SSIS.
* No meio, a superfície de design, com várias guias. Geralmente, você usa pelo menos as guias **Fluxo de Controle** e **Fluxo de Dados**.
* À direita, os painéis **Gerenciador de Soluções** e **Propriedades**.
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a>Etapa 2: criar o fluxo de dados básico
1. Arraste uma Tarefa Fluxo de Dados da Caixa de ferramentas até o centro da superfície de design (na guia **Fluxo de Controle**).
   
    ![][02]
2. Clique duas vezes na Tarefa Fluxo de Dados para mudar para a guia Fluxo de Dados.
3. Na lista Outras Fontes, da Caixa de ferramentas, arraste uma Fonte do ADO.NET até a superfície de design. Mantendo o adaptador de fonte selecionado, altere o nome dele para **fonte do SQL Server** no painel **Propriedades**.
4. Na lista Outros Destinos, na Caixa de ferramentas, arraste um Destino do ADO.NET até a superfície de design, na fonte do ADO.NET. Mantendo o adaptador de destino selecionado, altere o nome dele para **destino do SQL DW** no painel **Propriedades**.
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a>Etapa 3: configurar o adaptador de fonte
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

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a>Etapa 4: conectar o adaptador de fonte ao adaptador de destino
1. Selecione o adaptador de fonte na superfície de design.
2. Selecione a seta azul que se estende do adaptador de fonte e arraste-a até o editor de destino até que ela se encaixe.
   
    ![][10]
   
    Em um pacote do SSIS típico, você pode usar uma variedade de componentes adicionais da Caixa de ferramentas do SSIS entre a fonte e o destino para reestruturar, transformar e limpar seus dados, conforme eles passam pelo fluxo de dados do SSIS. Para deixar este exemplo o mais simples possível, estamos conectando a fonte diretamente com o destino.

## <a name="step-5-configure-the-destination-adapter"></a>Etapa 5: configurar o adaptador de destino
1. Clique duas vezes no adaptador de destino para abrir o **Editor de Destino ADO.NET**.
   
    ![][11]
2. Na guia **Gerenciador de Conexões** do **Editor de Destino ADO.NET**, clique no botão **Novo** próximo à lista do **Gerenciador de conexões** para abrir a caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET** e criar configurações de conexão para o banco de dados do SQL Data Warehouse do Azure, no qual este tutorial carrega os dados.
3. Na caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET**, clique no botão **Novo** para abrir a caixa de diálogo **Gerenciador de Conexões** e criar uma conexão de dados.
4. Na caixa de diálogo **Gerenciador de Conexões**, faça o seguinte.
   1. Para **Provedor**, selecione o Provedor de Dados SqlClient.
   2. Para **Nome do servidor**, digite o nome do SQL Data Warehouse.
   3. Na seção **Fazer logon no servidor**, selecione **Usar autenticação do SQL Server** e insira as informações de autenticação.
   4. Na seção **Conectar a um banco de dados**, selecione um banco de dados do SQL Data Warehouse existente.
   5. Clique em **Testar Conexão**.
   6. Na caixa de diálogo que relata os resultados do teste de conexão, clique em **OK** para retornar para a caixa de diálogo **Gerenciador de Conexões**.
   7. Na caixa de diálogo **Gerenciador de Conexões**, clique em **OK** para retornar para a caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET**.
5. Na caixa de diálogo **Configurar Gerenciador de Conexões ADO.NET**, clique em **OK** para retornar para o **Editor de Destino ADO.NET**.
6. No **Editor de Destino ADO.NET**, clique em **Novo**, ao lado da lista **Usar uma tabela ou exibição**, para abrir a caixa de diálogo **Criar Tabela** e criar uma tabela de destino com uma lista de colunas que corresponda à tabela de origem.
   
    ![][12a]
7. Na caixa de diálogo **Criar Tabela**, faça o seguinte.
   
   1. Altere o nome da tabela de destino para **SalesOrderDetail**.
   2. Remova a coluna **rowguid**. O tipo de dados **uniqueidentifier** não é compatível com o SQL Data Warehouse.
   3. Altere o tipo de dados da coluna **LineTotal** para **money**. O tipo de dados **decimal** não é compatível com o SQL Data Warehouse. Para obter informações sobre tipos de dados compatíveis, veja [CREATE TABLE (SQL Data Warehouse do Azure, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Clique em **OK** para criar a tabela e retornar ao **Editor de Destino ADO.NET**.
8. No **Editor de Destino ADO.NET**, selecione a guia **Mapeamentos** para ver como as colunas da fonte são mapeadas para as colunas do destino.
   
    ![][13]
9. Clique em **OK** para terminar a configuração da fonte de dados.

## <a name="step-6-run-the-package-to-load-the-data"></a>Etapa 6: executar o pacote para carregar os dados
Execute o pacote clicando no botão **Iniciar** na barra de ferramentas ou selecionando uma das opções **Executar** do menu **Depurar**.

Conforme o pacote começar a executar, você verá rodas amarelas giratórias indicando a atividade, bem como o número de linhas processadas até aquele momento.

![][14]

Quando a execução do pacote for concluída, você verá marcas de seleção verdes para indicar êxito, bem como o número total de linhas de dados carregados da fonte para o destino.

![][15]

Parabéns! Você conseguiu usar o SQL Server Integration Services para carregar dados no SQL Data Warehouse do Azure.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o fluxo de dados do SSIS. Comece aqui: [Fluxo de dados][Data Flow].
* Saiba como depurar e solucionar problemas de pacotes diretamente no ambiente de design. Comece aqui: [Ferramentas de solução de problemas para desenvolvimento de pacotes][Troubleshooting Tools for Package Development].
* Saiba como implantar seus pacotes e projetos do SSIS no servidor do Integration Services ou em outro local de armazenamento. Comece aqui: [Implantação de projetos e pacotes][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/load-data-to-sql-data-warehouse/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-data-warehouse/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-data-warehouse/test-connection-06.png
[07]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-data-warehouse/preview-data-08.png
[09]:  ./media/load-data-to-sql-data-warehouse/source-destination-09.png
[10]:  ./media/load-data-to-sql-data-warehouse/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-data-warehouse/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-data-warehouse/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-data-warehouse/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-data-warehouse/column-mapping-13.png
[14]:  ./media/load-data-to-sql-data-warehouse/package-running-14.png
[15]:  ./media/load-data-to-sql-data-warehouse/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: ../relational-databases/polybase/polybase-guide.md
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: ../t-sql/statements/create-table-azure-sql-data-warehouse.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
