---
title: Versões anteriores do SSDT (SQL Server Data Tools)
description: Saiba quais versões do SSDT e do SSDT-BI funcionam com quais versões do Visual Studio. Veja como instalar versões diferentes do SSDT e do SSDT-BI.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 5d32e301-0f44-4916-b0db-76e8322c0ab7
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 06/17/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=azuresqldb-mi-current'
ms.openlocfilehash: 35c16a4184665052781ae88ad37635ede298d668
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440489"
---
# <a name="previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi"></a>Versões anteriores do SQL Server Data Tools (SSDT e SSDT-BI)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

O SSDT (SQL Server Data Tools) fornece modelos de projeto e superfícies de design para a criação de tipos de conteúdo do SQL Server, tais como bancos de dados relacionais, modelos do Analysis Services, relatórios do Reporting Services e pacotes do Integration Services.

O SSDT é compatível com versões anteriores, assim, sempre será possível usar o [SSDT mais recente](download-sql-server-data-tools-ssdt.md) para criar e implantar bancos de dados, modelos, relatórios e pacotes para execução em versões anteriores do SQL Server.

Historicamente, o shell do Visual Studio usado para criar tipos de conteúdo do SQL Server foi lançado sob vários nomes, incluindo **SQL Server Data Tools**, **SQL Server Data Tools - Business Intelligence** e **Business Intelligence Development Studio**. Versões anteriores vinham com conjuntos distintos de modelos de projeto. Para obter todos os modelos de projeto juntos em um SSDT, você precisa da [versão mais recente](download-sql-server-data-tools-ssdt.md). Caso contrário, você provavelmente precisará instalar várias versões anteriores para obter todos os modelos usados no SQL Server. Apenas um shell será instalado por versão do Visual Studio; a instalação de um segundo SSDT apenas acrescenta os modelos que estavam faltando.

## <a name="previous-ssdt-releases"></a>Versões anteriores do SSDT

Baixe versões anteriores do SSDT selecionando o link de download na seção relacionada.

| Versão do SSDT | Versão do Visual Studio |
|--------------|-----------------------|
| [15.8](#ssdt-for-visual-studio-vs-2017) | 2017 |
| [17.4](#ssdt-for-visual-studio-vs-2015) | 2015 |
| [16.5](#ssdt-for-visual-studio-vs-2013) | 2013 |
| [11.1.50727.1](#ssdt-for-visual-studio-vs-2012) | 2012 |

### <a name="ssdt-for-visual-studio-vs-2017"></a>SSDT para VS (Visual Studio) 2017

**[Baixar o SSDT para Visual Studio 2017 (15.8)](https://go.microsoft.com/fwlink/?linkid=2124319)**

Esta versão do **SSDT para Visual Studio 2017** pode ser instalada nos seguintes idiomas:

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2124319&clcid=0x40a)

### <a name="ssdt-for-visual-studio-vs-2015"></a>SSDT para VS (Visual Studio) 2015

Para instalar esta versão do SSDT, é necessário baixar uma imagem ISO. O arquivo ISO é um arquivo autossuficiente que contém todos os componentes necessários ao SSDT e pode ser baixado com um gerenciador de download reiniciável, útil para situações com pouca ou limitada largura de banda de rede. Depois de baixado, o ISO pode ser montado como uma unidade.

Etapas da instalação:

1. **[Baixar o SSDT para Visual Studio 2015 (17.4)](https://go.microsoft.com/fwlink/?linkid=2132817)** .

2. Abra a imagem ISO.

3. Execute o arquivo *SSDTSetup.exe*.

    ![Imagem ISO](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

Esta versão do **SSDT para Visual Studio 2015** pode ser instalada nos seguintes idiomas:

| Linguagem | Hash SHA256 |
|----------|-------------|
| [Chinês (simplificado)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x804) | 79A958B122DDEC2857F1F4B9F0272A6BD2106BB17B4DA94CC68CACFCDDC16EAE |
| [Chinês (tradicional)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x404) | 8F9661883F2D2D28D6928AE66242DB465DBB25696EDFE0348D222421CEAB000A |
| [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x409) | 7727BA227A9E49C2DFCC1E9F2A10924CC472E3425653DC7DE8E4B830712B302E |
| [Francês](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x40c) | 2DF6655819F604E8D20A396CA9FDFEE279C5A9E50776FFC143A5BA4C3E2F1849 |
| [Alemão](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x407) | 5C44502DEE8B31675D0B10B4CE8CA6F5D96A2692CC498B9859A77C24F30EF870 |
| [Italiano](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x410) | 6A616F6E3A1C7DD52457FB8C8692E5C1C551032FF46AD8C5112CF9364F17C631 |
| [Japonês](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x411) | 1244A5EADF673E4BD36E9967A2008F65CA2A1D40E8E7DD4D17640A6FC1EACA9A |
| [Coreano](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x412) | 6E0E057A853F54AB87F3F8984954F590FCCD3BE2EC2139F02EFA085FEA6D3E61 |
| [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x416) | 24122C092464B299F41A7644814F375F0CC2786877BCAE0282221FF8D73BD100 |
| [Russo](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x419) | 2CDE208C241C3F13D2EC37294C10503C7A9D1222ED33F6FE54849169F30BE697 |
| [Espanhol](https://go.microsoft.com/fwlink/?linkid=2132817&clcid=0x40a) | BD12844E6F0A0ECFD5815D01EDFB8018CE9B4A1044DE8DF96AC740D85E800FD6 |

### <a name="ssdt-for-visual-studio-vs-2013"></a>SSDT para VS (Visual Studio) 2013

Para instalar esta versão do SSDT, é necessário baixar uma imagem ISO. O arquivo ISO é um arquivo autossuficiente que contém todos os componentes necessários ao SSDT e pode ser baixado com um gerenciador de download reiniciável, útil para situações com pouca ou limitada largura de banda de rede. Depois de baixado, o ISO pode ser montado como uma unidade.

Etapas da instalação:

1. **[Baixar o SSDT para Visual Studio 2013 (16.5)](https://go.microsoft.com/fwlink/?linkid=832312)**

2. Abra a imagem ISO.

3. Execute o arquivo *SSDTSetup.exe*.

    ![Imagem ISO](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

Esta versão do **SSDT para Visual Studio 2013** pode ser instalada nos seguintes idiomas:

| Linguagem | Hash SHA256 |
|----------|-------------|
| [Chinês (simplificado)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x804) | 79A958B122DDEC2857F1F4B9F0272A6BD2106BB17B4DA94CC68CACFCDDC16EAE |
| [Chinês (tradicional)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x404) | 8F9661883F2D2D28D6928AE66242DB465DBB25696EDFE0348D222421CEAB000A |
| [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x409) | 7727BA227A9E49C2DFCC1E9F2A10924CC472E3425653DC7DE8E4B830712B302E |
| [Francês](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x40c) | 2DF6655819F604E8D20A396CA9FDFEE279C5A9E50776FFC143A5BA4C3E2F1849 |
| [Alemão](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x407) | 5C44502DEE8B31675D0B10B4CE8CA6F5D96A2692CC498B9859A77C24F30EF870 |
| [Italiano](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x410) | 6A616F6E3A1C7DD52457FB8C8692E5C1C551032FF46AD8C5112CF9364F17C631 |
| [Japonês](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x411) | 1244A5EADF673E4BD36E9967A2008F65CA2A1D40E8E7DD4D17640A6FC1EACA9A |
| [Coreano](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x412) | 6E0E057A853F54AB87F3F8984954F590FCCD3BE2EC2139F02EFA085FEA6D3E61 |
| [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x416) | 24122C092464B299F41A7644814F375F0CC2786877BCAE0282221FF8D73BD100 |
| [Russo](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x419) | 2CDE208C241C3F13D2EC37294C10503C7A9D1222ED33F6FE54849169F30BE697 |
| [Espanhol](https://go.microsoft.com/fwlink/?linkid=832312&clcid=0x40a) | BD12844E6F0A0ECFD5815D01EDFB8018CE9B4A1044DE8DF96AC740D85E800FD6 |

### <a name="ssdt-for-visual-studio-vs-2012"></a>SSDT para VS (Visual Studio) 2012

Para instalar esta versão do SSDT, é necessário baixar uma imagem ISO. O arquivo ISO é um arquivo autossuficiente que contém todos os componentes necessários ao SSDT e pode ser baixado com um gerenciador de download reiniciável, útil para situações com pouca ou limitada largura de banda de rede. Depois de baixado, o ISO pode ser montado como uma unidade.

Etapas da instalação:

1. **[Baixar o SSDT para Visual Studio 2012 (11.1.50727.1)](https://go.microsoft.com/fwlink/?linkid=518814)**

2. Abra a imagem ISO.

3. Execute o arquivo *SSDTSetup.exe*.

    ![Imagem ISO](media/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi/iso-image.png)

Esta versão do **SSDT para Visual Studio 2012** pode ser instalada nos seguintes idiomas:

| Linguagem | Hash SHA256 |
|----------|-------------|
| [Chinês (simplificado)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x804) | 78F20325648CFF49D9C58A26186E0AC199D104B3CF634E5663B4B262BEC69C07 |
| [Chinês (tradicional)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x404) | A2722380AF2EE1E8BB52B4FA54A61BAB411E5E5FD5B050108F81ED23DC87366D |
| [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x409) | 748EF78D3F9CC6FE360432C378EA690DE51AEB2C747E87D43E08448D26F93A91 |
| [Francês](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x40c) | 40E6504169BF618EDC7EB5B62D1215DC96726D6EEC3CA8EC3EEB49044E4B6FB7 |
| [Alemão](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x407) | C45C974E6B8F9611BA2AC1EE90C5C507992BCE5693BF46F6C7C138591ED6A123 |
| [Italiano](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x410) | C1B20CDB41C7B1B5DE76A71F9A091A6FDF5186B12F6AA269DA6338B3CB2D91A6 |
| [Japonês](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x411) | BF56958B904C1C5F28084BD0B16928B6CBFEC83EB3F0C913EC364FA335241943 |
| [Coreano](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x412) | 9023B0656785C357A67E39EB76A2806B923C2BD17342D7226A8ADA384A9F4E28 |
| [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x416) | ACAD9FE03729E289ECE821D92C56CFB1D7FCCEA8423ABF1E164BF3C67ABEFEFB |
| [Russo](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x419) | E2191D787BA833DF4A85B064C5373DC44099E76214FBF9505728702D4D6B83F0 |
| [Espanhol](https://go.microsoft.com/fwlink/?linkid=518814&clcid=0x40a) | 6D81FB572A7003C54C29D2ACF076D2CED4A1CA80F329BFF9D41A806920D64EEE |

> [!Note]
> O SSDT dá suporte às duas versões mais recentes do Visual Studio. Com o lançamento do Visual Studio 2019, as versões do SSDT para Visual Studio 2015 e anteriores deixaram de ser atualizadas. O SSDT para Visual Studio 2010 não está mais disponível. Para obter mais informações, confira a seção *Perguntas frequentes* [desta postagem no blog da equipe do SSDT](/archive/blogs/ssdt/sql-server-data-tools-17-0-rc-and-ssdt-in-vs2017).

## <a name="sql-bi-analysis-services-reporting-services-integration-services"></a>SQL BI: Analysis Services, Reporting Services, Integration Services

Modelos de BI são usados para criar modelos do SSAS, relatórios do SSRS e pacotes do SSIS. Os designers de BI estão vinculados a versões específicas do SQL Server. Para usar os recursos de BI mais recentes, instale uma versão mais recente do designer de BI.

## <a name="bi-designers"></a>Designers de BI

[Baixar o SSDT-BI para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313) (SQL Server 2014, SQL Server 2012, SQL Server 2008 e 2008 R2)

[Baixar o SSDT-BI para Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843) (SQL Server 2014, SQL Server 2012, SQL Server 2008 e 2008 R2)

O Business Intelligence Development Studio (BIDS) é instalado por meio da instalação do SQL Server. Não há nenhum download da Web (SQL Server 2008 e 2008 R2).

Para o SQL Server 2012 ou 2014, você pode usar o **SSDT-BI para Visual Studio 2012** ou o **SSDT-BI fou o Visual Studio 2013**. A única diferença entre os dois é a versão do Visual Studio.

## <a name="next-steps"></a>Próximas etapas

- [Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [Notas sobre a versão do SSDT (SQL Server Data Tools)](release-notes-ssdt.md)
- [Baixar o SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- [Baixar o Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)
- [Ferramentas e utilitários do SQL](../tools/overview-sql-tools.md)