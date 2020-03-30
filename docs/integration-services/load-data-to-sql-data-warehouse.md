---
title: Carregar dados no SQL Data Warehouse do Azure com o SSIS (SQL Server Integration Services) | Microsoft Docs
description: Mostra como criar um pacote do SSIS (SQL Server Integration Services) para mover dados de uma ampla variedade de fontes de dados para o SQL Data Warehouse do Azure.
documentationcenter: NA
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
ms.custom: loading
ms.date: 08/09/2018
ms.author: chugu
author: chugugrace
ms.openlocfilehash: 3609de02157637ec30f7e21ad4426c5001f31a6e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71282654"
---
# <a name="load-data-into-azure-sql-data-warehouse-with-sql-server-integration-services-ssis"></a>Carregar dados no SQL Data Warehouse do Azure com o SSIS (SQL Server Integration Services)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Criar um pacote do SSIS (SQL Server Integration Services) para carregar dados no [SQL Data Warehouse do Azure](/azure/sql-data-warehouse/index). Opcionalmente, você pode reestruturar, transformar e limpar os dados conforme eles passam pelo fluxo de dados do SSIS.

Este artigo mostra como fazer o seguinte:

* Criar um projeto do Integration Services no Visual Studio.
* Criar um pacote do SSIS que carrega dados da fonte para o destino.
* Executar o pacote do SSIS para carregar os dados.

## <a name="basic-concepts"></a>Conceitos básicos

O pacote é a unidade básica de trabalho no SSIS. Os pacotes relacionados são agrupados em projetos. Você cria projetos e elabora pacotes no Visual Studio com o SQL Server Data Tools. O processo de design é um processo visual em que você arrasta e solta componentes da Caixa de ferramentas na superfície de design, conecta-os e define as respectivas propriedades. Depois de concluir seu pacote, você poderá executá-lo e, opcionalmente, implantá-lo no SQL Server ou no Banco de Dados SQL para realizar gerenciamento, monitoramento e segurança abrangentes.

Uma introdução detalhada ao SSIS está além do escopo deste artigo. Para saber mais, leia os seguintes artigos:

- [SQL Server Integration Services](sql-server-integration-services.md)

- [Como criar um pacote ETL](ssis-how-to-create-an-etl-package.md)

## <a name="options-for-loading-data-into-sql-data-warehouse-with-ssis"></a>Opções de carregamento de dados no SQL Data Warehouse com o SSIS
O SSIS (SQL Server Integration Services) é um conjunto flexível de ferramentas que oferece uma variedade de opções para se conectar ao SQL Data Warehouse e carregar dados nele.

1. O método preferencial, que fornece o melhor desempenho, é criar um pacote que use a [tarefa de upload do SQL DW do Azure](control-flow/azure-sql-dw-upload-task.md) para carregar os dados. Essa tarefa encapsula informações de origem e destino. Ela pressupõe que seus dados de origem são armazenados localmente em arquivos de texto delimitado.

2. Como alternativa, você pode criar um pacote que usa uma tarefa de fluxo de dados que contém uma origem e um destino. Essa abordagem dá suporte a uma ampla variedade de fontes de dados, incluindo SQL Server e SQL Data Warehouse do Azure.

## <a name="prerequisites"></a>Prerequisites
Para realizar este tutorial, você precisa do seguinte:

1. **Do SSIS (SQL Server Integration Services)** . O SSIS é um componente do SQL Server e requer uma versão licenciada, ou uma versão de avaliação ou do desenvolvedor, do SQL Server. Para obter uma versão de avaliação do SQL Server, consulte [Avaliar SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm).
2. **Visual Studio** (opcional). Para obter o Visual Studio Community Edition gratuito, confira [Visual Studio Community][Visual Studio Community]. Se não quiser instalar o Visual Studio, você poderá instalar apenas o SSDT (SQL Server Data Tools). O SSDT instala uma versão do Visual Studio com funcionalidade limitada.
3. **Do SSDT (SQL Server Data Tools) para Visual Studio**. Para obter o SQL Server Data Tools para Visual Studio, confira [Baixar o SSDT (SQL Server Data Tools)][Download SQL Server Data Tools (SSDT)].
4. **Um banco de dados do SQL Data Warehouse do Azure e permissões**. Este tutorial se conecta a uma instância do SQL Data Warehouse e carrega dados nela. Você precisa das permissões para se conectar, criar uma tabela e carregar dados.

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

## <a name="option-1---use-the-sql-dw-upload-task"></a>Opção 1 – Usar a tarefa de upload do SQL DW

A primeira abordagem é um pacote que usa a tarefa de upload do SQL DW. Essa tarefa encapsula informações de origem e destino. Ela pressupõe que seus dados de origem são armazenados em arquivos de texto delimitado, localmente ou no Armazenamento de Blobs do Azure.

### <a name="prerequisites-for-option-1"></a>Pré-requisitos para a Opção 1

Para continuar o tutorial com essa opção, você precisa do seguinte:

- O [Feature Pack do Microsoft SQL Server Integration Services para Azure][Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]. A tarefa de upload do SQL DW é um componente do Feature Pack.

- Uma conta de [Armazenamento de Blobs do Azure](https://docs.microsoft.com/azure/storage/). A tarefa de upload do SQL DW carrega dados do Armazenamento de Blobs do Azure para o SQL Data Warehouse do Azure. Você pode carregar arquivos que já estão no Armazenamento de Blobs ou pode carregar arquivos do seu computador. Se selecionar arquivos em seu computador, a tarefa de upload do SQL DW carregará, primeiramente, os arquivos no Armazenamento de Blobs para preparo e, em seguida, carregará os arquivos no SQL Data Warehouse.

### <a name="add-and-configure-the-sql-dw-upload-task"></a>Adicionar e configurar a tarefa de upload do SQL DW

1. Arraste uma tarefa de upload do SQL DW da caixa de ferramentas até o centro da superfície de design (na guia **Fluxo de controle**).

2. Clique duas vezes na tarefa para abrir o **editor da tarefa de upload do SQL DW**.

    ![Página geral do editor da tarefa de upload do SQL DW](media/load-data-to-sql-data-warehouse/azure-sql-dw-upload-task-editor.png)

3. Configure a tarefa com a ajuda das diretrizes no artigo [tarefa de upload do SQL DW do Azure](control-flow/azure-sql-dw-upload-task.md). Como essa tarefa encapsula as informações de origem e destino, bem como os mapeamentos entre tabelas de origem e destino, o editor da tarefa tem várias páginas de configurações para definir.

### <a name="create-a-similar-solution-manually"></a>Criar uma solução semelhante manualmente

Para obter mais controle, você pode criar manualmente um pacote que emula o trabalho realizado pela tarefa de upload do SQL DW. 

1. Use a Tarefa de upload de Blobs do Azure para preparar os dados no Armazenamento de Blobs do Azure. Para obter a tarefa de Upload de Blobs do Azure, baixe o [Feature Pack do Microsoft SQL Server Integration Services para Azure][Microsoft SQL Server 2017 Integration Services Feature Pack for Azure].

2. Depois, use a tarefa Executar SQL do SSIS para inicializar um script do PolyBase que carrega os dados no SQL Data Warehouse. Para obter um exemplo que carrega os dados do Armazenamento de Blobs do Azure no SQL Data Warehouse (mas não com o SSIS), consulte [Tutorial: carregar dados no SQL Data Warehouse do Azure](/azure/sql-data-wAREHOUSE/load-data-wideworldimportersdw).

## <a name="option-2---use-a-source-and-destination"></a>Opção 2 – Usar uma origem e um destino

A segunda abordagem é um pacote típico que usa uma tarefa de fluxo de dados que contém uma origem e um destino. Essa abordagem dá suporte a uma ampla variedade de fontes de dados, incluindo SQL Server e SQL Data Warehouse do Azure.

Este tutorial usa o SQL Server como fonte de dados. O SQL Server é executado localmente ou em uma máquina virtual do Azure.

Para se conectar ao SQL Server e ao SQL Data Warehouse, você pode usar um gerenciador de conexões ADO.NET e um destino e uma origem ou um gerenciador de conexões OLE DB e uma origem e um destino. Este tutorial usa o ADO.NET porque ele tem menos opções de configuração. O OLE DB pode resultar em um desempenho ligeiramente melhor do que o ADO.NET.

Como atalho, é possível usar o Assistente de Importação e Exportação do SQL Server para criar o pacote básico. Em seguida, salve o pacote e abra-o no Visual Studio ou no SSDT para exibi-lo e personalizá-lo. Para obter mais informações, consulte [Importar e exportar dados com o Assistente para Importação e Exportação do SQL Server](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

### <a name="prerequisites-for-option-2"></a>Pré-requisitos para a Opção 2

Para continuar o tutorial com essa opção, você precisa do seguinte:

1. **De dados de exemplo**. Este tutorial usa dados de exemplo armazenados no SQL Server, no banco de dados de exemplo AdventureWorks, como os dados de origem a serem carregados no SQL Data Warehouse. Para obter o banco de dados de exemplo AdventureWorks, confira [Bancos de dados de exemplo AdventureWorks][AdventureWorks 2014 Sample Databases].

2. **De uma regra de firewall**. Você precisa criar uma regra de firewall no SQL Data Warehouse com o endereço IP do seu computador local antes de carregar dados no SQL Data Warehouse.

### <a name="create-the-basic-data-flow"></a>Criar o fluxo de dados básico
1. Arraste uma Tarefa Fluxo de Dados da Caixa de ferramentas até o centro da superfície de design (na guia **Fluxo de Controle**).
   
    ![][02]
2. Clique duas vezes na Tarefa Fluxo de Dados para mudar para a guia Fluxo de Dados.
3. Na lista Outras Fontes, da Caixa de ferramentas, arraste uma Fonte do ADO.NET até a superfície de design. Mantendo o adaptador de fonte selecionado, altere o nome dele para **fonte do SQL Server** no painel **Propriedades**.
4. Na lista Outros Destinos, na Caixa de ferramentas, arraste um Destino do ADO.NET até a superfície de design, na fonte do ADO.NET. Mantendo o adaptador de destino selecionado, altere o nome dele para **destino do SQL DW** no painel **Propriedades**.
   
    ![][09]

### <a name="configure-the-source-adapter"></a>Configurar o adaptador de fonte
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

### <a name="connect-the-source-adapter-to-the-destination-adapter"></a>Conectar o adaptador de fonte ao adaptador de destino
1. Selecione o adaptador de fonte na superfície de design.
2. Selecione a seta azul que se estende do adaptador de fonte e arraste-a até o editor de destino até que ela se encaixe.
   
    ![][10]
   
    Em um pacote do SSIS típico, você pode usar uma variedade de componentes adicionais da Caixa de ferramentas do SSIS entre a fonte e o destino para reestruturar, transformar e limpar seus dados, conforme eles passam pelo fluxo de dados do SSIS. Para deixar este exemplo o mais simples possível, estamos conectando a fonte diretamente com o destino.

### <a name="configure-the-destination-adapter"></a>Configurar o adaptador de destino
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
   3. Altere o tipo de dados da coluna **LineTotal** para **money**. O tipo de dados **decimal** não é compatível com o SQL Data Warehouse. Para saber mais sobre tipos de dados compatíveis, confira [CREATE TABLE (SQL Data Warehouse do Azure, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Clique em **OK** para criar a tabela e retornar ao **Editor de Destino ADO.NET**.
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

Parabéns! Você conseguiu usar o SQL Server Integration Services para carregar dados no SQL Data Warehouse do Azure.

## <a name="next-steps"></a>Próximas etapas

- Saiba como depurar e solucionar problemas de pacotes diretamente no ambiente de design. Comece aqui: [Solução de problemas de ferramentas para o desenvolvimento de pacotes][Troubleshooting Tools for Package Development].

- Saiba como implantar seus pacotes e projetos do SSIS no servidor do Integration Services ou em outro local de armazenamento. Comece por aqui: [Implantação de projetos e pacotes][Deployment of Projects and Packages].

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
[Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]: https://www.microsoft.com/download/details.aspx?id=54798
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2017
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
