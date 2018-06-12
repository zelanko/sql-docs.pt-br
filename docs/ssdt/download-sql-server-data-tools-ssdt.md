---
title: Baixar o SSDT (SQL Server Data Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology: ssdt
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- instalar o ssdt, baixar o ssdt, ssdt mais recente
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6794784b2339fe9c246dc4aec017e4e7cbb93311
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773332"
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

[![baixar](../ssdt/media/download.png) Baixar o SSDT para Visual Studio 2017 (15.7.0) ](https://go.microsoft.com/fwlink/?linkid=874716) 

> [!IMPORTANT]
> Antes de instalar o SSDT para o Visual Studio 2017 (15.7.0), desinstale as extensões "Projetos do Microsoft Analysis Services" e "Projetos do Microsoft Reporting Services", caso elas já estejam instaladas e feche todas as instâncias do VS. 



**Informações da versão**  
  
Número da versão: 15.7.0  
Número de build: 14.0.16165.0  
Data do lançamento: 1 de junho de 2018  

Para obter uma lista completa das alterações, consulte o [log de mudanças](changelog-for-sql-server-data-tools-ssdt.md).

O SSDT para Visual Studio 2017 tem os mesmos [requisitos de sistema](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs) que o Visual Studio.  

### <a name="available-languages---ssdt-for-vs-2017"></a>Idiomas disponíveis – SSDT para VS 2017

Esta versão do **SSDT para VS 2017** pode ser instalada nos seguintes idiomas:  

[Chinês (República Popular da China)]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x804) | 
[Chinês (Taiwan)]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x404) | 
[Inglês (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x409) | 
[Francês]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x40c)  
[Alemão]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x407) | 
[Italiano]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x410) | 
[Japonês]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x411) | 
[Coreano]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x412) | 
[Português (Brasil)]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x416) | 
[Russo]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x419) | 
[Espanhol]( https://go.microsoft.com/fwlink/?linkid=874716&clcid=0x40a)  



## <a name="ssdt-for-vs-2015-standalone-installer"></a>SSDT para VS 2015 (instalador autônomo)

[![download](../ssdt/media/download.png) Baixar o SSDT para Visual Studio 2015 (17.4)](https://go.microsoft.com/fwlink/?linkid=863440)

**Informações da versão**  
  
O número da versão: 17.4

O número de build desta versão: 14.0.61712.050
  
Para obter uma lista completa das alterações, consulte o [log de mudanças](changelog-for-sql-server-data-tools-ssdt.md).

### <a name="available-languages---ssdt-for-vs-2015"></a>Idiomas disponíveis – SSDT para VS 2015
  
Esta versão do **SSDT para VS 2015** pode ser instalada nos seguintes idiomas:  

[Chinês (República Popular da China)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x804) | 
[Chinês (Taiwan)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x404) | 
[Inglês (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x409) | 
[Francês]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x40c)  
[Alemão]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x407) | 
[Italiano]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x410) | 
[Japonês]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x411) | 
[Coreano]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x412) | 
[Português (Brasil)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x416) | 
[Russo]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x419) | 
[Espanhol]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x40a)  

### <a name="iso-images---ssdt-for-vs-2015"></a>Imagens ISO – SSDT para VS 2015

Uma imagem ISO do SSDT pode ser usada como uma alternativa para instalar o SSDT ou configurar um ponto de instalação administrativa. O ISO é um arquivo autossuficiente que contém todos os componentes necessários ao SSDT e pode ser baixado com um gerenciador de download reiniciável, útil para situações com pouca ou limitada largura de banda de rede. Depois de baixado, o ISO poderá ser montado como uma unidade ou gravado em um DVD.

> [!NOTE]
> As imagens ISO do SSDT para VS 2015 17.4 agora estão disponíveis.

[Chinês (República Popular da China)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x804) |
[Chinês (Taiwan)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x404) |
[Inglês (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x409) |
[Francês]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x40c)  
[Alemão]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x407) |
[Italiano]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x410) |
[Japonês]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x411) |
[Coreano]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x412) |
[Português (Brasil)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x416) |
[Russo]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x419) |
[Espanhol]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x40a)



## <a name="supported-sql-versions"></a>Versões do SQL com suporte
  
|Modelos de projeto|Plataformas SQL com suporte|  
|-------------------|--------------------|  
Bancos de dados relacionais|  SQL Server 2005* – SQL Server 2017<br> (use o SSDT 17.x ou o SSDT para Visual Studio 2017 para conectar-se ao [SQL Server no Linux](../linux/sql-server-linux-overview.md))<br /><br />Banco de dados SQL do Azure<br /><br />SQL Data Warehouse do Azure (dá suporte somente a consultas; ainda não há suporte para projetos de banco de dados)<br /><br />  * O suporte ao SQL Server 2005 está preterido,<br /><br /> passe para uma versão do SQL oficialmente com suporte|
  |Modelos do Analysis Services<br /><br />Relatórios do Reporting Services | SQL Server 2008 – SQL Server 2017|
  |pacotes do Integration Services| SQL Server 2012 – SQL Server 2017    |
  
## <a name="dacfx"></a>DacFx
O SSDT para Visual Studio 2015 e o SSDT para Visual Studio 2017 usam o DacFx 17.4.1: [baixar o DacFx (Data-Tier Application Framework) 17.4.1](https://www.microsoft.com/download/details.aspx?id=56508).


## <a name="next-steps"></a>Próximas etapas  
Depois de instalar o SSDT, trabalhe com esses tutoriais para aprender a criar bancos de dados, pacotes, modelos de dados e relatórios usando o SSDT:  

- [Desenvolvimento de banco de dados offline orientado a projetos](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
- [Tutorial SSIS: Criando um pacote ETL simples](../integration-services/ssis-how-to-create-an-etl-package.md)  
- [Tutoriais do Analysis Services](../analysis-services/analysis-services-tutorials-ssas.md)  
- [Criando um relatório de tabela básico (Tutorial do SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]


## <a name="see-also"></a>Consulte Também  
[SQL Server Data Tools no Visual Studio](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[Fórum do MSDN do SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog da equipe do SSDT](http://blogs.msdn.com/b/ssdt/)  
[Documentação do SSDT](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[Referência DACFx API](https://msdn.microsoft.com/library/dn645454.aspx)  
[Baixar o SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  