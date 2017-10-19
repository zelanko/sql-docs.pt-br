---
title: Importar de uma fonte de dados relacional (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: d45d72ca09a8abce6d29f018fcbaa8f54415a637
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="import-data---relational-data-source"></a>Importar dados - fonte de dados relacional
  Para modelos de tabela na 1200 e níveis de compatibilidade inferiores, você pode importar dados de uma variedade de bancos de dados relacionais usando o Assistente de importação de tabela. O assistente está disponível em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no menu **Modelo** . Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador. Para obter mais informações sobre os provedores e as fontes de dados com suporte, consulte [Fontes de dados com suporte &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md). 
 
 O Assistente de Importação de Tabela dá suporte a importação de dados das seguintes fontes de dados:  
  
 **Bancos de dados relacionais**  
  
-   Banco de dados do Microsoft SQL Server  
  
-   Microsoft SQL Azure  
  
-   Bancos de dados do Microsoft Access  
  
-   Microsoft SQL Server Parallel Data Warehouse  
  
-   Oracle  
  
-   Teradata  
  
-   Sybase  
  
-   Informix  
  
-   IBM DB2  
  
-   OLE DB/ODBC  
  
 **Origens multidimensionais**  
  
-   Cubo do Microsoft SQL Server Analysis Services  
  
 O Assistente de Importação de Tabela não dá suporte a importação de dados de uma Pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como uma fonte de dados.  
  
### <a name="to-import-data-from-a-database"></a>Para importar dados de um banco de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**.  
  
2.  Na página **Conectar com uma Fonte de Dados** , selecione o tipo de banco de dados ao qual se conectar e clique em **Avançar**.  
  
3.  Siga as etapas no Assistente de Importação de Tabela. Nas páginas subsequentes, você poderá selecionar tabelas específicas e exibições ou aplicar filtros usando a página **Selecionar Tabelas e Exibições** ou criando uma consulta SQL na página **Especificar uma Consulta SQL** .  
  
## <a name="see-also"></a>Consulte também  
 [Importar dados &#40;SSAS de Tabela&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Fontes de dados com suporte &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  

