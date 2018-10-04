---
title: Fontes de dados com suporte (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 606d597bd539da9e50b1c0452d9126e2f4671731
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054366"
---
# <a name="data-sources-supported-ssas-tabular"></a>Fontes de dados com suporte (SSAS tabular)
  Este tópico descreve os tipos de fonte de dados que podem ser usados com modelos tabulares.  
  
 Este artigo inclui as seções a seguir:  
  
-   [Fontes de dados com suporte](#bkmk_supported_ds)  
  
-   [Não há suporte para fontes](#bkmk_unsupported_ds)  
  
-   [Dicas para escolher fontes de dados](#bkmk_tips)  
  
##  <a name="bkmk_supported_ds"></a> Fontes de dados com suporte  
 Você pode importar dados das fontes de dados na tabela a seguir: Quando você instalar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a instalação não instala os provedores listados para cada fonte de dados. Alguns deles podem já estar instalados com outros aplicativos no computador; em outros casos, você precisará baixar e instalar o provedor.  
  
|||||  
|-|-|-|-|  
|Origem|Versões|Tipo de arquivo|Provedores <sup>1</sup>|  
|Bancos de dados do Access|Microsoft Access 2003, 2007, 2010.|.accdb ou .mdb|Provedor OLE DB ACE 14|  
|Bancos de dados relacionais do SQL Server|Microsoft SQL Server 2005, 2008, 2008 R2; SQL Server 2012, o Microsoft SQL Azure banco de dados <sup>2</sup>|(não se aplica)|Provedor OLE DB para SQL Server<br /><br /> Provedor OLE DB do SQL Server Native Client<br /><br /> Provedor OLE DB do SQL Server Native 10.0 Client<br /><br /> Provedor de dados .NET Framework para SQL Client|  
|SQL Server Parallel Data Warehouse (PDW) <sup>3</sup>|2008 R2|(não se aplica)|Provedor OLE DB para SQL Server PDW|  
|Bancos de dados relacionais da Oracle|Oracle 9i, 10g, 11g.|(não se aplica)|Provedor OLE DB Oracle<br /><br /> Provedor de Dados .NET Framework para Cliente Oracle<br /><br /> Provedor de dados do .NET Framework para SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Bancos de dados relacionais do Teradata|Teradata V2R6, V12|(não se aplica)|Provedor OLE DB TDOLEDB<br /><br /> Provedor de .NET Data para Teradata|  
|Bancos de dados relacionais do Informix||(não se aplica)|Provedor OLE DB para Informix|  
|Bancos de dados relacionais IBM DB2|8.1|(não se aplica)|DB2OLEDB|  
|Bancos de dados relacionais do Sybase Adaptive Server Enterprise (ASE)|15.0.2|(não se aplica)|Provedor OLE DB para Sybase|  
|Outros bancos de dados relacionais|(não se aplica)|(não se aplica)|Provedor OLE DB para driver ODBC|  
|Arquivos de texto|(não se aplica)|.txt, .tab, .csv|Provedor OLE DB ACE 14 para Microsoft Access|  
|Arquivos do Microsoft Excel|Excel 97-2003, 2007, 2010|.xlsx, xlsm, .xlsb, .xltx, .xltm|Provedor OLE DB ACE 14|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pasta de trabalho|Microsoft SQL Server 2008 R2 Analysis Services|xlsx, xlsm, .xlsb, .xltx, .xltm|ASOLEDB 10.5<br /><br /> (usado apenas com pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] publicadas em farms do SharePoint com o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] instalado)|  
|Cubo do Analysis Services|Microsoft SQL Server 2005, 2008, 2008 R2 Analysis Services|(não se aplica)|ASOLEDB 10|  
|Alimentações de dados<br /><br /> (usado para importar dados de relatórios do Reporting Services, documentos do serviço Atom, Microsoft Azure Marketplace DataMarket e feed de dados único)|Formato Atom 1.0<br /><br /> Qualquer banco de dados ou documento exposto como um Serviço de dados do WCF (Windows Communication Foundation) (antes ADO.NET Data Services).|.atomsvc para um documento de serviço que define uma ou mais alimentações<br /><br /> .atom para um documento de feed da Web do Atom|Provedor de Feed de Dados Microsoft para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> Provedor de dados do feed de dados do .NET Framework para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Arquivos de conexão de banco de dados do Office||.odc||  
  
 <sup>1</sup> você também pode usar o provedor OLE DB para ODBC.  
  
 <sup>2</sup> para obter mais informações sobre o SQL Azure, consulte o site da web [SQL Azure](http://go.microsoft.com/fwlink/?LinkID=157856).  
  
 <sup>3</sup> para obter mais informações sobre o SQL Server PDW, consulte o site da web [SQL Server 2008 R2 Parallel Data Warehouse](http://go.microsoft.com/fwlink/?LinkId=150895).  
  
 <sup>4</sup> em alguns casos, usar o provedor OLE DB MSDAORA pode resultar em erros de conexão, especialmente com versões mais novas do Oracle. Se você encontrar algum erro, será recomendável usar um dos outros provedores listados para Oracle.  
  
##  <a name="bkmk_unsupported_ds"></a> Não há suporte para fontes  
 A seguinte fonte de dados não tem suporte no momento:  
  
-   Os documentos de servidor, como bancos de dados do Access já publicados no SharePoint, não podem ser importados.  
  
##  <a name="bkmk_tips"></a> Dicas para escolher fontes de dados  
  
1.  A importação de tabelas de bancos de dados relacionais elimina etapas pois são usadas relações de *chave estrangeira* durante a importação para criar relações entre as tabelas no designer de modelos.  
  
2.  Você também pode eliminar etapas com a importação de várias tabelas e a exclusão das tabelas desnecessárias. Se você importar uma tabela de cada vez, talvez ainda precise criar relações manualmente entre tabelas.  
  
3.  Colunas que contêm dados semelhantes em fontes de dados diferentes são a base para criar relações dentro do designer de modelos. Ao usar fontes de dados heterogêneos, escolha tabelas com colunas que possam ser mapeadas para tabelas em outras fontes de dados que contêm dados idênticos ou semelhantes.  
  
4.  Os provedores OLE DB às vezes podem oferecer desempenho mais rápido para dados em grande escala. Ao escolher entre diferentes provedores para a mesma fonte de dados, experimente primeiro o provedor OLE DB.  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados &#40;Tabular do SSAS&#41;](../data-sources-ssas-tabular.md)   
 [Importar dados &#40;Tabular do SSAS&#41;](../import-data-ssas-tabular.md)  
  
  
