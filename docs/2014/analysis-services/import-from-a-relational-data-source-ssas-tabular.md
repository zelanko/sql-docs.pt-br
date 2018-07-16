---
title: Importar de uma fonte de dados relacional (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61f5a7035f17848ead9a3133a2e5e22829099dab
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37204426"
---
# <a name="import-from-a-relational-data-source-ssas-tabular"></a>Importar de uma fonte de dados relacional (SSAS tabular)
  Você pode importar dados de uma variedade de bancos de dados relacionais usando o Assistente de Importação de Tabela. O assistente está disponível em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no menu **Modelo** . Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador. Para obter mais informações sobre os provedores e as fontes de dados com suporte, consulte [Data Sources Supported &#40;SSAS Tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md).  
  
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
  
 O Assistente de Importação de Tabela não dá suporte a importação de dados de uma Pasta de trabalho do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] como uma fonte de dados.  
  
### <a name="to-import-data-from-a-database"></a>Para importar dados de um banco de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**.  
  
2.  Na página **Conectar com uma Fonte de Dados** , selecione o tipo de banco de dados ao qual se conectar e clique em **Avançar**.  
  
3.  Siga as etapas no Assistente de Importação de Tabela. Nas páginas subsequentes, você poderá selecionar tabelas específicas e exibições ou aplicar filtros usando a página **Selecionar Tabelas e Exibições** ou criando uma consulta SQL na página **Especificar uma Consulta SQL** .  
  
## <a name="see-also"></a>Consulte também  
 [Importar dados &#40;Tabular do SSAS&#41;](import-data-ssas-tabular.md)   
 [Fontes de dados com suporte &#40;SSAS Tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
