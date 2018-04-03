---
title: Modelos de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 54cd62aa50aff198d2397843c528f09a1a2fc83b
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
---
# <a name="tabular-models"></a>Modelos de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Os modelos Tabulares são bancos de dados do Analysis Services que são executados na memória ou no modo DirectQuery, acessando os dados diretamente a partir de fontes de dados relacionais de back-end. Usando algoritmos de compactação de última geração e processador de consulta multi-threaded, o mecanismo de análise fornece acesso rápido a dados e objetos de modelo tabular relatando aplicativos cliente como o Power BI e Excel.  
  
 Embora modelos na memória são o padrão, o DirectQuery é um modo alternativo de consulta para modelos que são muito grandes para caber na memória, ou quando uma estratégia de processamento razoável impede a volatilidade dos dados. O DirectQuery atinge paridade com modelos na memória por meio do suporte para uma ampla variedade de fontes de dados, capacidade de lidar com tabelas calculadas e colunas em um modelo DirectQuery, a segurança em nível de linha por meio de expressões DAX que acessar o banco de dados de back-end e de consulta otimizações que resultam em uma taxa de transferência.
  
 Modelos de tabela são criados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando o modelo de projeto de modelo de tabela que fornece uma superfície de design para criar um modelo, tabelas, relações e expressões DAX. Você pode importar dados de várias origens e enriquecer o modelo adicionando relações, colunas e tabelas calculadas, medidas, KPIs, hierarquias e traduções.  
  
 Modelos podem ser implantados com o Azure Analysis Services ou uma instância do SQL Server Analysis Services configurada para modo de servidor Tabular. Modelos de tabela implantados podem ser gerenciados no SQL Server Management Studio. Como os modelos de crescem, podem ser particionados para processamento otimizado e protegidos para o nível de linha usando segurança baseada em função.  

  
  
