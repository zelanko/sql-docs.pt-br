---
title: Suporte para fontes de dados (SSAS - Multidimensional) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Analysis Services, data sources
- data sources [Analysis Services], about data sources
- Analysis Services, data sources
- connections [Analysis Services]
- SSAS, data sources
ms.assetid: c97e0f8d-7ddd-4941-8b51-e7832f30fbbe
caps.latest.revision: 69
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 173ba9ef24e1f05dcd3500ad8fecbad0dba98241
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="supported-data-sources-ssas---multidimensional"></a>Fontes de Dados com Suporte (SSAS - Multidimensional)
  Este tópico descreve os tipos de fonte de dados que você pode usar em um modelo multidimensional.  
  
##  <a name="bkmk_supported_ds"></a> Fontes de dados com suporte  
 Você pode recuperar dados das fontes de dados na tabela a seguir: Quando você instalar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a instalação não instala os provedores listados para cada fonte de dados. Alguns deles podem já estar instalados com outros aplicativos no computador; em outros casos, você precisará baixar e instalar o provedor.  
  
> [!NOTE]  
>  Também é possível usar provedores de outros fabricantes, como Oracle OLE DB Provider, na conexão com banco de dados de terceiros, com suporte fornecido por esses fabricantes.  
  
|||||  
|-|-|-|-|  
|Origem|Versões|Tipo de arquivo|Provedores*|  
|Bancos de dados do Access|Microsoft Access  2010, 2013, 2016|.accdb ou .mdb|Provedor OLE DB do Microsoft Jet 4.0|  
|Bancos de dados relacionais do SQL Server*|Microsoft SQL Server 2008, 2008 R2, 2012, 2014, 2016, [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] , Microsoft Analytics Platform System (APS)<br /><br /> <br /><br /> Observação: para obter mais informações sobre [!INCLUDE[ssSDS](../../includes/sssds-md.md)] no [Azure.com](http://go.microsoft.com/fwlink/?LinkID=157856).<br /><br /> Observação: o Analytics Platform System (APS) era anteriormente conhecido como SQL Server Parallel Datawarehouse (PDW). Originalmente, conectar o PDW a partir do Analysis Services exigia um provedor de dados especial. Esse provedor foi substituído no SQL Server 2012. A partir do SQL Server 2012, o cliente nativo do SQL Server é usado para as conexões com o PDW/APS. Para saber mais sobre o APS, acesse o site [Microsoft Analytics Platform System](http://www.microsoft.com/en-us/server-cloud/products/analytics-platform-system/resources.aspx).|(não se aplica)|Provedor OLE DB para SQL Server<br /><br /> Provedor OLE DB do SQL Server Native Client<br /><br /> Provedor OLE DB do SQL Server Native 11.0 Client<br /><br /> Provedor de dados .NET Framework para SQL Client|  
|Bancos de dados relacionais da Oracle|Oracle 9i, 10g, 11g, 12g|(não se aplica)|Provedor OLE DB Oracle<br /><br /> Provedor de Dados .NET Framework para Cliente Oracle<br /><br /> Provedor de dados do .NET Framework para SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Bancos de dados relacionais do Teradata|Teradata V2R6, V12|(não se aplica)|Provedor OLE DB TDOLEDB<br /><br /> Provedor de .NET Data para Teradata|  
|Bancos de dados relacionais do Informix|V11.10|(não se aplica)|Provedor OLE DB para Informix|  
|Bancos de dados relacionais IBM DB2|8.1|(não se aplica)|DB2OLEDB|  
|Bancos de dados relacionais do Sybase Adaptive Server Enterprise (ASE)|15.0.2|(não se aplica)|Provedor OLE DB para Sybase|  
|Outros bancos de dados relacionais|(não se aplica)|(não se aplica)|Um provedor de OLE DB|  
  
 \* Fontes de dados ODBC não têm suporte em soluções multidimensionais. Embora o próprio Analysis Services trate a conexão, os designers no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] usado para criar soluções não podem se conectar a uma fonte de dados ODBC, mesmo ao usar driver do MSDASQL. Se seus requisitos comerciais incluírem uma fonte de dados ODBC, crie uma solução tabelar em vez disso.  
  
 ** Alguns recursos requerem um banco de dados relacional do SQL Server executado localmente. Mais especificamente, os armazenamentos ROLAP e de write-back requerem que a fonte de dados subjacente seja um banco de dados relacional do SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados com suporte &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [Fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  

