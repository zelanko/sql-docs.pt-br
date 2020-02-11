---
title: Importar de uma fonte de dados relacional (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61fb30ea21ea810eab8d30a3a040fac4a1bd2128
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66080529"
---
# <a name="import-from-a-relational-data-source-ssas-tabular"></a>Importar de uma fonte de dados relacional (SSAS tabular)
  Você pode importar dados de uma variedade de bancos de dados relacionais usando o Assistente de Importação de Tabela. O assistente está disponível em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no menu **Modelo** . Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador. Para obter mais informações sobre os provedores e as fontes de dados com suporte, consulte [Fontes de dados com suporte &#40;SSAS de Tabela&#41;](tabular-models/data-sources-supported-ssas-tabular.md).  
  
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
  
 **Fontes multidimensionais**  
  
-   Cubo do Microsoft SQL Server Analysis Services  
  
 O Assistente de Importação de Tabela não dá suporte a importação de dados de uma Pasta de trabalho do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] como uma fonte de dados.  
  
### <a name="to-import-data-from-a-database"></a>Para importar dados de um banco de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**.  
  
2.  Na página **Conectar com uma Fonte de Dados** , selecione o tipo de banco de dados ao qual se conectar e clique em **Avançar**.  
  
3.  Siga as etapas no Assistente de Importação de Tabela. Nas páginas subsequentes, você poderá selecionar tabelas específicas e exibições ou aplicar filtros usando a página **Selecionar Tabelas e Exibições** ou criando uma consulta SQL na página **Especificar uma Consulta SQL** .  
  
## <a name="see-also"></a>Consulte Também  
 [Importar dados &#40;SSAS de tabela&#41;](import-data-ssas-tabular.md)   
 [Fontes de dados com suporte &#40;SSAS de tabela&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
