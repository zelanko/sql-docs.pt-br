---
title: Baixar o SSDT (SQL Server Data Tools) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
keywords:
- instalar o ssdt, baixar o ssdt, ssdt mais recente
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 703990d0484240d602c34ca24262df38e7aadc5b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736596"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>Baixar e instalar o SSDT (SQL Server Data Tools) para o Visual Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
O **SQL Server Data Tools** é uma moderna ferramenta de desenvolvimento para criar bancos de dados relacionais do SQL Server, bancos de dados SQL do Azure, modelos de dados do AS (Analysis Services), pacotes do IS (Integration Services) e relatórios do RS (Reporting Services). Com o SSDT, você pode projetar e implantar qualquer tipo de conteúdo do SQL Server com a mesma facilidade com que desenvolve um aplicativo no Visual Studio.

*Para a maioria dos usuários, o SSDT (SQL Server Data Tools) é instalado durante a instalação do Visual Studio. A instalação do SSDT usando o instalador do Visual Studio adiciona a funcionalidade básica do SSDT. Portanto, ainda é necessário executar o [instalador autônomo do SSDT](#ssdt-for-vs-2017-standalone-installer) para obter as ferramentas do AS, IS e RS.*

## <a name="install-ssdt-with-visual-studio-2017"></a>Instalar o SSDT com o Visual Studio 2017

Para instalar o SSDT durante a [instalação do Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio), selecione a carga de trabalho **Armazenamento e processamento de dados** e, em seguida, selecione **SQL Server Data Tools**. Se o Visual Studio já está instalado, é possível [editar a lista de cargas de trabalho](https://docs.microsoft.com/visualstudio/install/modify-visual-studio) para incluir o SSDT: ![Carga de trabalho Armazenamento e processamento de dados](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)



## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Instalar ferramentas do Analysis Services, do Integration Services e do Reporting Services
Para instalar suporte ao projeto do AS, do IS e do RS, execute o [instalador autônomo do SSDT](#ssdt-for-vs-2017-standalone-installer). 

O instalador lista instâncias disponíveis do Visual Studio às quais adicionar as ferramentas do SSDT. Se o Visual Studio não está instalado, ao selecionar **Instalar uma nova instância do SQL Server Data Tools**, o SSDT é instalado com um versão mínima do Visual Studio, mas para obter a melhor experiência, recomendamos usar o SSDT com [a versão mais recente do Visual Studio](https://www.visualstudio.com/downloads). 

![selecione AS, IS, RS](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)



## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT para VS 2017 (instalador autônomo)

[![download](../ssdt/media/download.png) Baixar o SSDT para Visual Studio 2017 (15.8.1) ](https://go.microsoft.com/fwlink/?linkid=2024393) 

> [!IMPORTANT]
> - Antes de instalar o SSDT para o Visual Studio 2017 (15.8.1), desinstale as extensões *Projetos do Analysis Services* e *Projetos do Reporting Services* caso elas já estejam instaladas e feche todas as instâncias do VS.
> - Ao instalar o SSDT no Windows 10 1803 e optar por instalar o SSIS, você pode encontrar uma reinicialização inesperada. Você pode iniciar o instalador novamente e continuar a instalação após a reinicialização.
> - No momento, o SSDT 15.8.1 não dá suporte ao Windows 7 SP1, portanto permaneça na versão 15.8.0 se você estiver usando o Windows 7 SP1.



**Informações da versão**  
  
Número da versão: 15.8.1  
Número de build: 14.0.16179.0  
Data de lançamento: 27 de setembro de 2018  

Para obter uma lista completa das alterações, consulte o [log de mudanças](changelog-for-sql-server-data-tools-ssdt.md).

O SSDT para Visual Studio 2017 tem os mesmos [requisitos de sistema](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs) que o Visual Studio.  

### <a name="available-languages---ssdt-for-vs-2017"></a>Idiomas disponíveis – SSDT para VS 2017

Esta versão do **SSDT para VS 2017** pode ser instalada nos seguintes idiomas:  

[Chinês (simplificado)]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x804) | 
[chinês (tradicional)]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x404) | 
[inglês (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x409) | 
[francês]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x40c)  
[Alemão]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x407) | 
[Italiano]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x410) | 
[Japonês]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x411) | 
[Coreano]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x412) | 
[Português (Brasil)]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x416) | 
[Russo]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x419) | 
[Espanhol]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x40a)  


## <a name="offline-install"></a>Instalação offline

Para instalar o SSDT quando você não estiver conectado à Internet, siga as etapas nesta seção. Para obter mais informações, confira [Criar uma instalação de rede do Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio).

Primeiro, conclua as etapas a seguir enquanto estiver online:

1. [Baixe o instalador autônomo do SSDT](#ssdt-for-vs-2017-standalone-installer).
2. [Baixe o vs_sql.exe](https://aka.ms/vs/15/release/vs_sql.exe).
3. Enquanto estiver online, execute um dos comandos a seguir para baixar todos os arquivos necessários para a instalação offline. Usar a opção `--layout` é a chave. Substitua <filepath> pelo caminho real para salvar os arquivos.

   A.   Para um idioma específico, passe a localidade: `vs_sql.exe --layout c:\<filepath> --lang en-us` (um único idioma tem aproximadamente 1 GB)  
   B. Para todos os idiomas, omita o argumento `--lang`: `vs_sql.exe --layout c:\<filepath>` (todos os idiomas têm aproximadamente 3.9 GB).

Depois de concluir as etapas anteriores, o seguinte pode ser realizado enquanto estiver offline:

1. Copie o conteúdo do VS2017 para a pasta de conteúdo do SSDT. Verifique se todos os arquivos de ambos são combinados em uma única pasta de layouts.
2. Execute `vs_setup.exe --NoWeb` para instalar o Shell do VS2017 e o projeto de dados do SQL Server.
3. Execute `SSDT-Setup-ENU.exe /install` e selecione SSIS/SSRS/SSAS.

   - Ou para uma instalação autônoma, execute `SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive`  

Para ver as opções disponíveis, execute `SSDT-Setup-ENU.exe /help`

## <a name="supported-sql-versions"></a>Versões do SQL com suporte
  
|Modelos de projeto|Plataformas SQL com suporte|  
|-------------------|--------------------|  
Bancos de dados relacionais|  SQL Server 2005* – SQL Server 2017<br> (use o SSDT 17.x ou o SSDT para Visual Studio 2017 para conectar-se ao [SQL Server no Linux](../linux/sql-server-linux-overview.md))<br /><br />Banco de dados SQL do Azure<br /><br />SQL Data Warehouse do Azure (dá suporte somente a consultas; ainda não há suporte para projetos de banco de dados)<br /><br />  * O suporte ao SQL Server 2005 está preterido,<br /><br /> passe para uma versão do SQL oficialmente com suporte|
  |Modelos do Analysis Services<br /><br />Relatórios do Reporting Services | SQL Server 2008 – SQL Server 2017|
  |pacotes do Integration Services| SQL Server 2012 – SQL Server 2017    |
  
## <a name="dacfx"></a>DacFx
O SSDT para Visual Studio 2015 e o SSDT para Visual Studio 2017 usam o DacFx 17.4.1: [baixar o DacFx (Data-Tier Application Framework) 17.4.1](https://www.microsoft.com/download/details.aspx?id=56508).

## <a name="previous-versions"></a>Versões anteriores

Para baixar e instalar o SSDT para o Visual Studio 2015 ou uma versão mais antiga de SSDT, confira [Versões anteriores do SQL Server Data Tools (SSDT e SSDT-BI)](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md).



## <a name="next-steps"></a>Próximas etapas  
Depois de instalar o SSDT, trabalhe com esses tutoriais para aprender a criar bancos de dados, pacotes, modelos de dados e relatórios usando o SSDT:  

- [Desenvolvimento de banco de dados offline orientado a projetos](project-oriented-offline-database-development.md)  
- [Tutorial SSIS: Criando um pacote ETL simples](../integration-services/ssis-how-to-create-an-etl-package.md)  
- [Tutoriais do Analysis Services](../analysis-services/analysis-services-tutorials-ssas.md)  
- [Criando um relatório de tabela básico (Tutorial do SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]


## <a name="see-also"></a>Consulte Também  
[Fórum do MSDN do SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog da equipe do SSDT](http://blogs.msdn.com/b/ssdt/)  
[Referência DACFx API](https://msdn.microsoft.com/library/dn645454.aspx)  
[Baixar o SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
