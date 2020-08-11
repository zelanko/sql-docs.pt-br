---
title: Baixar o SQL Server Data Tools (SSDT)
description: Saiba mais sobre o SSDT (SQL Server Data Tools). Veja como instalar esse conjunto de ferramentas de desenvolvimento de banco de dados com o Visual Studio 2019 e o Visual Studio 2017.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssdt
ms.topic: conceptual
keywords: instalar o ssdt, baixar o ssdt, ssdt mais recente
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 02/20/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: dbaaa71b61129d0bb1917644c017122e6ed88bf4
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2020
ms.locfileid: "86278996"
---
# <a name="download-sql-server-data-tools-ssdt-for-visual-studio"></a>Baixe o SSDT (SQL Server Data Tools) para Visual Studio

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

O **SSDT (SQL Server Data Tools)** é uma moderna ferramenta de desenvolvimento para criar bancos de dados relacionais do SQL Server, Bancos de Dados SQL do Azure, modelos de dados do AS (Analysis Services), pacotes do IS (Integration Services) e relatórios do RS (Reporting Services). Com o SSDT, você pode projetar e implantar qualquer tipo de conteúdo do SQL Server com a mesma facilidade com que desenvolve um aplicativo no Visual Studio.

## <a name="ssdt-for-visual-studio-2019"></a>SSDT para Visual Studio 2019

### <a name="changes-in-ssdt-for-visual-studio-2019"></a>Alterações no SSDT para Visual Studio 2019

A principal funcionalidade do SSDT para criar projetos de banco de dados permaneceu integralmente no Visual Studio.

Com o Visual Studio de 2019, a funcionalidade necessária para habilitar os projetos do Analysis Services, do Integration Services e do Reporting Services foi movida para as respectivas extensões VSIX (Visual Studio) somente.

> [!NOTE]
> Não existe um instalador autônomo do SSDT para o Visual Studio 2019.

### <a name="install-ssdt-with-visual-studio-2019"></a>Instalar o SSDT com o Visual Studio 2019

Se o [Visual Studio 2019](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2019) já estiver instalado, você poderá editar a lista de cargas de trabalho para incluir o SSDT. Caso não tenha o Visual Studio 2019 instalado, você pode baixar e instalar o [Visual Studio 2019 Community](https://visualstudio.microsoft.com/downloads/).

* Para projetos de Banco de Dados SQL, selecione **SQL Server Data Tools** em **Armazenamento e processamento de dados** na lista de cargas de trabalho.

   ![Carga de trabalho de armazenamento e processamento de dados](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload-2019.png)

* Para os projetos do Analysis Services, do Integration Services ou do Reporting Services, você pode instalar as [extensões](https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions) apropriadas em *Ferramentas > Extensões e Atualizações* ou no [Marketplace](https://marketplace.visualstudio.com/search?term=services&target=VS&category=All%20categories&vsVersion=&sortBy=Relevance).

* [Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

* [Serviços de Integração](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects)

* [Reporting Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)

## <a name="ssdt-for-visual-studio-2017"></a>SSDT para Visual Studio 2017

### <a name="changes-in-ssdt-for-visual-studio-2017"></a>Alterações no SSDT para Visual Studio 2017

Iniciando no Visual Studio 2017, foi integrada a funcionalidade de criação de Projetos de banco de dados na instalação do Visual Studio. Não é necessário executar o instalador autônomo do SSDT na experiência principal do SSDT.

Agora para criar projetos do Analysis Services, do Integration Services ou do Reporting Services, você ainda precisa do instalador autônomo do SSDT.

### <a name="install-ssdt-with-visual-studio-2017"></a>Instalar o SSDT com o Visual Studio 2017

Para instalar o SSDT durante a [instalação do Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio), selecione a carga de trabalho **Armazenamento e processamento de dados** e, em seguida, selecione **SQL Server Data Tools**.

Se o Visual Studio já estiver instalado, você poderá [editar a lista de cargas de trabalho](https://docs.microsoft.com/visualstudio/install/modify-visual-studio) para incluir o SSDT.

![Carga de trabalho de armazenamento e processamento de dados](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload-2017.png)

### <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Instalar ferramentas do Analysis Services, do Integration Services e do Reporting Services

Para instalar suporte a um projeto do Analysis Services, do Integration Services e do Reporting Services, execute o [instalador autônomo do SSDT](#ssdt-for-vs-2017-standalone-installer).

O instalador lista instâncias disponíveis do Visual Studio para adicionar as ferramentas do SSDT. Se o Visual Studio ainda não estiver instalado, selecionar **Instalar uma nova instância do SQL Server Data Tools** instalará o SSDT com uma versão mínima do Visual Studio, mas para obter a melhor experiência, recomendamos usar o SSDT com [a versão mais recente do Visual Studio](https://www.visualstudio.com/downloads).

![Selecione AS, IS, RS](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)

## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT para VS 2017 (instalador autônomo)

:::image type="icon" source="media/download.png" border="false"::: **[Baixar o SSDT para Visual Studio 2017 (15.9.5)](https://go.microsoft.com/fwlink/?linkid=2131035)**

> [!IMPORTANT]
> * Antes de instalar o SSDT para Visual Studio 2017 (15.9.5), desinstale as extensões *Projetos do Analysis Services* e *Projetos do Reporting Services* caso já estejam instaladas e feche todas as instâncias do VS. 
> * O componente de caixa de entrada Origem do Power Query para SQL Server 2017 foi removido. Agora, anunciamos a Origem do Power Query para SQL Server 2017 e 2019 como componente pronto para uso, que pode ser baixado [aqui](https://www.microsoft.com/download/details.aspx?id=100619).
> * Para criar pacotes usando os conectores Oracle e Teradata e direcionar uma versão anterior do SQL Server antes do SQL 2019, além do [Microsoft Oracle Connector para SQL 2019](https://www.microsoft.com/download/details.aspx?id=58228) e [Microsoft Teradata Connector para SQL 2019](https://www.microsoft.com/download/details.aspx?id=100599), você também precisa instalar a versão correspondente do Microsoft Connector para Oracle e Teradata do Attunity.
>    * [Microsoft Connector versão 5.0 para Oracle e Teradata da Attunity direcionado ao SQL Server 2017](https://www.microsoft.com/download/details.aspx?id=55179)
>    * [Microsoft Connector versão 4.0 para Oracle e Teradata da Attunity direcionado ao SQL Server 2016](https://www.microsoft.com/download/details.aspx?id=52950)
>    * [Microsoft Connector versão 3.0 para Oracle e Teradata da Attunity direcionado ao SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=44582)
>    * [Microsoft Connector versão 2.0 para Oracle e Teradata da Attunity direcionado ao SQL Server 2012](https://www.microsoft.com/download/details.aspx?id=29283)

### <a name="release-notes"></a>Notas de versão

Para obter uma lista completa de alterações, confira [Notas sobre a versão para o SSDT (SQL Server Data Tools)](release-notes-ssdt.md).

### <a name="system-requirements"></a>Requisitos do sistema

O SSDT para Visual Studio 2017 tem os mesmos [requisitos de sistema](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs) que o Visual Studio.

### <a name="available-languages---ssdt-for-vs-2017"></a>Idiomas disponíveis – SSDT para VS 2017

Esta versão do **SSDT para VS 2017** pode ser instalada nos seguintes idiomas:

* [Chinês (simplificado)](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x804)
* [Chinês (tradicional)](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x404)
* [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x409)
* [Francês](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x40c)
* [Alemão](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x407)
* [Italiano](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x410)
* [Japonês](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x411)
* [Coreano](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x412)
* [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x416)
* [Russo](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x419)
* [Espanhol](https://go.microsoft.com/fwlink/?linkid=2131035&clcid=0x40a)

### <a name="considerations-and-limitations"></a>Considerações e limitações

* Não é possível instalar a versão da comunidade estando offline

* Para atualizar o SSDT, você precisará seguir o mesmo caminho utilizado para instalar o SSDT. Por exemplo, se você tiver adicionado o SSDT usando as extensões do VSIX, deverá atualizar por meio das extensões do VSIX. Se você instalou o SSDT por meio de uma instalação separada, você precisa atualizá-lo usando esse método.

## <a name="offline-install"></a>Instalação offline

Para instalar o SSDT quando você não estiver conectado à Internet, siga as etapas nesta seção. Para obter mais informações, confira [Criar uma instalação de rede do Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio).

Primeiro, conclua as etapas a seguir enquanto estiver **online**:

1. [Baixe o instalador autônomo do SSDT](#ssdt-for-vs-2017-standalone-installer).

2. [Baixe o vs_sql.exe](https://aka.ms/vs/15/release/vs_sql.exe).

3. Enquanto estiver online, execute um dos comandos a seguir para baixar todos os arquivos necessários para a instalação offline. Usar a opção `--layout` como chave, faz com que os arquivos reais para instalação offline sejam baixados. Substitua `<filepath>` pelo demarcador de layouts real para salvar os arquivos.
   1. Para um idioma específico, passe a localidade: `vs_sql.exe --layout c:\<filepath> --lang en-us` (um único idioma tem aproximadamente 1 GB).
   1. Para todos os idiomas, omita o argumento `--lang`: `vs_sql.exe --layout c:\<filepath>` (todos os idiomas têm aproximadamente 3,9 GB).

Depois de concluir as etapas anteriores, as seguintes etapas podem ser realizadas enquanto estiver **offline**:

1. Execute `vs_setup.exe --NoWeb` para instalar o Shell do VS2017 e o projeto de dados do SQL Server.

2. Na pasta de layouts, execute `SSDT-Setup-ENU.exe /install` e selecione o SSIS/SSRS/SSAS.
   a. Para uma instalação autônoma, execute `SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive`.

Para ver as opções disponíveis, execute `SSDT-Setup-ENU.exe /help`

> [!NOTE]
> Se você usar uma versão completa do Visual Studio 2017, crie uma pasta offline somente para o SSDT e execute `SSDT-Setup-ENU.exe` nessa pasta recém-criada (não adicione o SSDT em outro layout offline do Visual Studio 2017). Se você adicionar o layout do SSDT a um layout offline do Visual Studio existente, os componentes de runtime necessários (.exe) não serão criados lá.

## <a name="supported-sql-versions"></a>Versões do SQL com suporte

|Modelos de projeto|Plataformas SQL com suporte|
|-------------------|--------------------|
|Bancos de dados relacionais| SQL Server 2005\* – SQL Server 2017<br> (use o SSDT 17.x ou o SSDT para Visual Studio 2017 para conectar-se ao [SQL Server no Linux](../linux/sql-server-linux-overview.md))<br /><br />Banco de Dados SQL do Azure<br /><br />SQL Data Warehouse do Azure (dá suporte somente a consultas; ainda não há suporte para projetos de banco de dados)<br /><br /> \* O suporte ao SQL Server 2005 está preterido,<br /><br /> passe para uma versão do SQL oficialmente com suporte|
|Modelos do Analysis Services<br /><br />Relatórios do Reporting Services | SQL Server 2008 – SQL Server 2017|
|pacotes do Integration Services| SQL Server 2012 – SQL Server 2019 |

## <a name="dacfx"></a>DacFx

Os SSDTs para Visual Studio 2015 e 2017 usam DacFx 17.4.1: [Baixar a estrutura de aplicativo da camada de dados (DacFx) 17.4.1](https://www.microsoft.com/download/details.aspx?id=56508).

## <a name="previous-versions"></a>Versões anteriores

Para baixar e instalar o SSDT para o Visual Studio 2015 ou uma versão mais antiga de SSDT, confira [Versões anteriores do SQL Server Data Tools (SSDT e SSDT-BI)](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md).

## <a name="see-also"></a>Consulte Também

* [Fórum do MSDN do SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt) 

* [Blog da equipe do SSDT](https://blogs.msdn.com/b/ssdt/)

* [Referência DACFx API](https://msdn.microsoft.com/library/dn645454.aspx)

* [Baixar o SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)

## <a name="next-steps"></a>Próximas etapas

Depois de instalar o SSDT, trabalhe com esses tutoriais para aprender a criar bancos de dados, pacotes, modelos de dados e relatórios usando o SSDT.

* [Desenvolvimento de banco de dados offline orientado a projetos](project-oriented-offline-database-development.md)

* [Tutorial do SSIS: criar um pacote ETL simples](../integration-services/ssis-how-to-create-an-etl-package.md)

* [Tutoriais do Analysis Services](https://docs.microsoft.com/analysis-services/analysis-services-tutorials-ssas)

* [Criando um relatório de tabela básico (Tutorial do SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
