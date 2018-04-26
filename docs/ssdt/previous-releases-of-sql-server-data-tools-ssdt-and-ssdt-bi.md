---
title: Versões anteriores do SQL Server Data Tools (SSDT e SSDT-BI) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2018
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5d32e301-0f44-4916-b0db-76e8322c0ab7
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c7ffd5758be12f1999169b6b77558395925395af
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi"></a>Versões anteriores do SQL Server Data Tools (SSDT e SSDT-BI)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
O SQL Server Data Tools (SSDT) fornece modelos de projeto e superfícies de design para a criação de tipos de conteúdo do SQL Server, como bancos de dados relacionais, modelos do Analysis Services, relatórios do Reporting Services e pacotes do Integration Services.  
  
Ele tem com base um shell do Visual Studio e é lançado junto com o SQL Server. Novas versões do SSDT integram os recursos mais recentes do SQL Server. As versões mais antigas incluem os modelos e o ambiente de design que eram atuais naquela versão.  
  
O SSDT é compatível com versões anteriores, assim, sempre será possível usar o [SSDT mais recente](download-sql-server-data-tools-ssdt.md) para criar e implantar bancos de dados, modelos, relatórios e pacotes para execução em versões anteriores do SQL Server.  
  
> [!NOTE]  
> Historicamente, o shell do Visual Studio usado para criar tipos de conteúdo do SQL Server foi lançado sob vários nomes, incluindo **SQL Server Data Tools**, **SQL Server Data Tools - Business Intelligence**e **Business Intelligence Development Studio**. Versões anteriores vinham com conjuntos distintos de modelos de projeto. Para obter todos os modelos de projeto juntos em um SSDT, você precisa da [versão mais recente](download-sql-server-data-tools-ssdt.md). Caso contrário, você provavelmente precisará instalar várias versões anteriores para obter todos os modelos usados no SQL Server.  Apenas um shell será instalado por versão do Visual Studio; a instalação de um segundo SSDT apenas acrescenta os modelos que estavam faltando.  

## <a name="recent-downloads"></a>Downloads recentes

Os últimos downloads são fornecidos no caso pouco provável de você enfrentar problemas com a [versão mais recente](download-sql-server-data-tools-ssdt.md). 

|Versão| Visual Studio 2017|
|:---|:---|
|15.5.2|[SSDT para VS2017 15.5.2](https://go.microsoft.com/fwlink/?LinkId=866452)|
|15.5.1|[SSDT para VS2017 15.5.1](https://go.microsoft.com/fwlink/?LinkId=865748)|  
<br>


|Versão| Visual Studio 2015|
|:---|:---|
|17.3|[SSDT para VS2015 17.3](https://go.microsoft.com/fwlink/?linkid=858660)| 
|17.2|[SSDT para VS2015 17.2](https://go.microsoft.com/fwlink/?linkid=852922)| 
|17.1|[SSDT para VS2015 17.1](https://go.microsoft.com/fwlink/?linkid=849393)|
|17.0|[SSDT para VS2015 17.0](https://go.microsoft.com/fwlink/?linkid=846626)| 
|16.5|[SSDT para VS2015 16.5](https://go.microsoft.com/fwlink/?LinkID=832313)|  
<br>

|Versão| Visual Studio 2013|
|:---|:---|
|16.5|[SSDT para VS2013 16.5](https://go.microsoft.com/fwlink/?LinkID=832308)|  
<br>


\* O SSDT oferece suporte às duas versões mais recentes do Visual Studio. Com a versão do Visual Studio 2017, o SSDT para VS2013 não será atualizado novamente. Para obter mais informações, consulte a seção *perguntas frequentes* [desta postagem do blog da equipe do SSDT](https://blogs.msdn.microsoft.com/ssdt/2017/03/10/sql-server-data-tools-17-0-rc-and-ssdt-in-vs2017/).

  
## <a name="links-to-download-pages"></a>Links para páginas de download 
**Relacional do SQL: mecanismo de banco de dados**  
  
Fornece modelos para criar bancos de dados relacionais para o RDBMS e o Banco de Dados SQL do Microsoft Azure. O SSDT é independente de versão em relação ao design do banco de dados relacional. Você pode usar a versão do Visual Studio 2012 ou 2013 com qualquer versão do Mecanismo de Banco de Dados do SQL Server ou do Banco de Dados SQL do Microsoft Azure.  
  
**Designers de banco de dados**  
  
-   [Baixar o SSDT para Visual Studio 2013](https://msdn.microsoft.com/dn864412)  
  
-   [Baixar o SSDT para Visual Studio 2012](https://msdn.microsoft.com/jj650015)  
  
-   O**SSDT para Visual Studio 2010** não está mais disponível. Escolha uma versão mais recente. As versões mais recentes do SSDT podem ser executadas lado a lado com as instalações existentes do Visual Studio 2010. Não é necessário que o SSDT corresponda à versão completa do produto do Visual Studio em seu computador.  
  
Os clientes do Visual Studio 2013 podem baixar uma versão de visualização do SSDT para experimentar os novos recursos que ainda não estão na versão de lançamento do produto.  
  
**SQL BI: Analysis Services, Reporting Services, Integration Services**  
  
Modelos de BI são usados para criar modelos do SSAS, relatórios do SSRS e pacotes do SSIS. Os designers de BI estão vinculados a versões específicas do SQL Server. Para usar os recursos de BI mais recentes, instale uma versão mais recente do designer de BI.  
  
**Designers de BI**  
  
[Baixar o SSDT-BI para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313) (SQL Server 2014, SQL Server 2012, SQL Server 2008 e 2008 R2)  
  
[Baixar o SSDT-BI para Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843) (SQL Server 2014, SQL Server 2012, SQL Server 2008 e 2008 R2)  
  
O Business Intelligence Development Studio (BIDS) é instalado por meio da instalação do SQL Server. Não há nenhum download da Web. (SQL Server 2008 e 2008 R2)  
  
Para o SQL Server 2012 ou 2014, você pode usar o **SSDT-BI para Visual Studio 2012** ou o **SSDT-BI fou o Visual Studio 2013**. A única diferença entre os dois é a versão do Visual Studio.  
  
## <a name="see-also"></a>Consulte Também  
[Baixar o SQL Server Data Tools &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[Baixar o SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[Ferramentas e utilitários do SQL](../tools/overview-sql-tools.md)
