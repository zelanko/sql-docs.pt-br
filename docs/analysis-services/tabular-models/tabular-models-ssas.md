---
title: Modelos de tabela | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e85a618379b5b3c6da010c8b25782ed6836edb4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="tabular-models"></a>Modelos de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Os modelos Tabulares são bancos de dados do Analysis Services que são executados na memória ou no modo DirectQuery, acessando os dados diretamente a partir de fontes de dados relacionais de back-end. Usando algoritmos de compactação de última geração e processador de consulta multi-threaded, o mecanismo de análise fornece acesso rápido a dados e objetos de modelo tabular relatando aplicativos cliente como o Power BI e Excel.  
  
 Embora modelos na memória são o padrão, o DirectQuery é um modo alternativo de consulta para modelos que são muito grandes para caber na memória, ou quando uma estratégia de processamento razoável impede a volatilidade dos dados. O DirectQuery atinge paridade com modelos na memória por meio do suporte para uma ampla variedade de fontes de dados, capacidade de lidar com tabelas calculadas e colunas em um modelo DirectQuery, a segurança em nível de linha por meio de expressões DAX que acessar o banco de dados de back-end e de consulta otimizações que resultam em uma taxa de transferência.
  
 Modelos de tabela são criados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando o modelo de projeto de modelo de tabela que fornece uma superfície de design para criar um modelo, tabelas, relações e expressões DAX. Você pode importar dados de várias origens e enriquecer o modelo adicionando relações, colunas e tabelas calculadas, medidas, KPIs, hierarquias e traduções.  
  
 Modelos podem ser implantados com o Azure Analysis Services ou uma instância do SQL Server Analysis Services configurada para modo de servidor Tabular. Modelos de tabela implantados podem ser gerenciados no SQL Server Management Studio. Como os modelos de crescem, podem ser particionados para processamento otimizado e protegidos para o nível de linha usando segurança baseada em função.  

  
  
