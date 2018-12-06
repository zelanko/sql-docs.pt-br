---
title: Versões anteriores do SQL Server Data Tools (SSDT e SSDT-BI) | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 5d32e301-0f44-4916-b0db-76e8322c0ab7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 39f2ebeca9f19c8c00707c9e5427c797dfc09881
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52519756"
---
# <a name="previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi"></a>Versões anteriores do SQL Server Data Tools (SSDT e SSDT-BI)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
O SSDT (SQL Server Data Tools) fornece modelos de projeto e superfícies de design para a criação de tipos de conteúdo do SQL Server, tais como bancos de dados relacionais, modelos do Analysis Services, relatórios do Reporting Services e pacotes do Integration Services.  
  
O SSDT é compatível com versões anteriores, assim, sempre será possível usar o [SSDT mais recente](download-sql-server-data-tools-ssdt.md) para criar e implantar bancos de dados, modelos, relatórios e pacotes para execução em versões anteriores do SQL Server.  
  
> [!NOTE]  
> Historicamente, o shell do Visual Studio usado para criar tipos de conteúdo do SQL Server foi lançado sob vários nomes, incluindo **SQL Server Data Tools**, **SQL Server Data Tools - Business Intelligence**e **Business Intelligence Development Studio**. Versões anteriores vinham com conjuntos distintos de modelos de projeto. Para obter todos os modelos de projeto juntos em um SSDT, você precisa da [versão mais recente](download-sql-server-data-tools-ssdt.md). Caso contrário, você provavelmente precisará instalar várias versões anteriores para obter todos os modelos usados no SQL Server.  Apenas um shell será instalado por versão do Visual Studio; a instalação de um segundo SSDT apenas acrescenta os modelos que estavam faltando.  

## <a name="recent-downloads"></a>Downloads recentes

Os últimos downloads são fornecidos no caso pouco provável de você enfrentar problemas com a versão mais recente.

|Versão do SSDT| Visual Studio 2017|
|:---|:---|
|15.8.0|[SSDT para VS2017 15.8.0](https://go.microsoft.com/fwlink/?linkid=2014060)|
|15.7.1|[SSDT para VS2017 15.7.1](https://go.microsoft.com/fwlink/?LinkId=875613)|
|15.7.0|[SSDT para VS2017 15.7.0](https://go.microsoft.com/fwlink/?LinkId=874716)|
|15.6.0|[SSDT para VS2017 15.6.0](https://go.microsoft.com/fwlink/?LinkId=871368)|
<br>

|Versão do SSDT| Visual Studio 2015|
|:---|:---|
|17.4|[SSDT para VS2015 17.4](https://go.microsoft.com/fwlink/?linkid=863440)|
|17.3|[SSDT para VS2015 17.3](https://go.microsoft.com/fwlink/?linkid=858660)|
|16.5|[SSDT para VS2015 16.5](https://go.microsoft.com/fwlink/?LinkID=832313)|  
<br>

|Versão do SSDT| Visual Studio 2013|
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
