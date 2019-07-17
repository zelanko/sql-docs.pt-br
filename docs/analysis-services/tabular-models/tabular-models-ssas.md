---
title: Modelos de tabela no Analysis Services | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae7dfd78e71c41ab5b826a27742923445117417d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162430"
---
# <a name="tabular-models"></a>Modelos de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Modelos tabulares no Analysis Services são os bancos de dados que são executados na memória ou no modo DirectQuery, conexão a dados diretamente a partir de dados relacionais de back-end fontes. Usando algoritmos de compactação de última geração e processador de consulta multi-threaded, o mecanismo de análise de Vertipaq do Analysis Services entrega acesso rápido a objetos e dados modelo tabular relatando aplicativos clientes, como o Power BI e Excel.  
  
 Embora modelos na memória são padrão, o DirectQuery é um modo alternativo de consulta para modelos que são muito grandes para caber na memória, ou quando uma estratégia de processamento razoável impede a volatilidade dos dados. DirectQuery atinge paridade com modelos na memória por meio do suporte para uma ampla variedade de fontes de dados, capacidade de lidar com tabelas calculadas e colunas em um modelo DirectQuery, a segurança em nível de linha por meio de expressões DAX que acessar o banco de dados de back-end e de consulta otimizações que resultam em taxa de transferência mais rápida.
  
 Modelos de tabela são criados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando o modelo de projeto de modelo de tabela. O modelo de projeto fornece uma superfície de design para criar objetos de modelo semântico como tabelas, partições, relações, hierarquias, medidas e KPIs. 
  
 Modelos de tabela podem ser implantados ao Azure Analysis Services ou uma instância do SQL Server Analysis Services está configurado para o modo de servidor de tabela. Modelos de tabela implantados podem ser gerenciados no SQL Server Management Studio. 

Modelagem de tabela inclui a documentação aqui se aplica, na maioria dos casos, ao SQL Server Analysis Services e o Azure Analysis Services. Artigos específicos para o Azure Analysis Services são publicados juntamente com outras documentações do Azure. Para obter mais informações, consulte [documentação do Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/).
  
