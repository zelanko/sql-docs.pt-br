---
title: Importar dados (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6617b2a2-9f69-433e-89e0-4c5dc92982cf
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fc8728c2a4e023fb03e0e2de8e3c457e0f15fd72
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122945"
---
# <a name="import-data-ssas-tabular"></a>Importar dados (SSAS tabular)
  Você pode importar dados para o modelo de tabela de uma ampla variedade de origens. Os tópicos nesta seção descrevem como usar o Assistente de Importação de Dados para o qual conectar e selecionar dados a serem importados para um projeto de modelo.  
  
> [!IMPORTANT]  
>  Se alguma das tabelas em seu modelo contiver um número grande de linhas, importe somente um subconjunto dos dados durante a criação do modelo. Ao importar um subconjunto dos dados, você poderá reduzir o tempo de processamento e o consumo de recursos do servidor de banco de dados do espaço de trabalho.  
  
 Usando o Assistente de Importação de Tabela, você pode importar dados das seguintes fontes de dados:  
  
|**Fonte de dados**|**Descrição**|  
|---------------------|---------------------|  
|**Bancos de dados relacionais**|As fontes de dados relacionais incluem:<br /><br /> Microsoft SQL Server<br /><br /> Microsoft SQL Azure<br /><br /> Microsoft SQL Server Parallel Data Warehouse<br /><br /> Microsoft Access<br /><br /> Oracle<br /><br /> Teradata<br /><br /> Sybase<br /><br /> Informix<br /><br /> IBM DB2<br /><br /> OLEDB/ODBC|  
|**Origens multidimensionais**|Cubo do Microsoft SQL Server Analysis Services|  
|**Feeds de dados**|Feeds de dados incluem:<br /><br /> Relatório do Microsoft Reporting Services<br /><br /> Conjunto de dados do Azure DataMarket<br /><br /> Feeds atom de um provedor público ou corporativo|  
|**Arquivos de texto**|Arquivos de texto incluem:<br /><br /> Arquivos do Excel (.xlsx)<br /><br /> Arquivo de Texto (.txt)|  
  
 Além de importar dados usando o Assistente de Importação de Tabela, você pode colar dados copiados (da Área de Transferência) em uma tabela. Os dados colados comportam-se diferentemente de dados que foram importados de outras fontes de dados. Os dados colados em tabelas não têm uma propriedade Nome de Conexão ou Dados de Origem. Dados colados são persistidos no arquivo Model.bim. Quando o projeto ou o arquivo Model.bim for salvo, os dados colados também serão salvos.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Importar de uma fonte de dados relacional &#40;Tabular do SSAS&#41;](import-from-a-relational-data-source-ssas-tabular.md)|Descreve como importar dados de fontes de dados relacionais como um banco de dados Microsoft SQL Server, Oracle ou Teradata.|  
|[Importar de uma fonte de dados multidimensionais &#40;Tabular do SSAS&#41;](import-from-a-multidimensional-data-source-ssas-tabular.md)|Descreve como importar dados de um cubo multidimensional do SQL Server Analysis Services.|  
|[Importar de um Feed de dados &#40;Tabular do SSAS&#41;](import-from-a-data-feed-ssas-tabular.md)|Descreve como importar dados de um feed de dados como um relatório do Microsoft Reporting Services ou conjunto de dados Azure Data Market.|  
|[Importar de um arquivo de texto &#40;Tabular do SSAS&#41;](import-from-a-text-file-ssas-tabular.md)|Descreve como importar dados de uma pasta de trabalho do Microsoft Excel ou arquivo de texto.|  
|[Copiar e colar dados &#40;Tabular do SSAS&#41;](copy-and-paste-data-ssas-tabular.md)|Descreve como acrescentar dados a uma tabela existente no designer modelo usando Colar e Colar Acréscimo.|  
  
  