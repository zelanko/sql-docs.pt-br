---
title: "Objetos (Analysis Services - dados multidimensionais) de dimensão | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: dimensions [Analysis Services], objects
ms.assetid: 7f3d55c7-cccb-4ad0-b6cb-3a2c9992dd68
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 90c27aef2c6c8584e5822bc05eb21147fde6022e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>Objetos de dimensão (Analysis Services - Dados Multidimensionais)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Um simples <xref:Microsoft.AnalysisServices.Dimension> objeto é composto por informações básicas, atributos e hierarquias. As informações básicas incluem o nome da dimensão, o tipo de dimensão, a fonte de dados, o modo de armazenamento e outros. Os atributos definem os dados reais na dimensão. Os atributos não necessariamente pertencem a uma hierarquia, mas hierarquias são criadas a partir de atributos. Uma hierarquia cria listas ordenadas de níveis e define os modos como um usuário pode explorar a dimensão.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir fornecem mais informações sobre como projetar e implementar objetos de dimensão.  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], dimensões são um componente fundamental dos cubos. As dimensões organizam dados com relação a uma área de interesse, como clientes, lojas ou funcionários, para usuários.|  
|[Atributos e hierarquias de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)|As dimensões são coleções de atributos, vinculados a uma ou mais colunas na tabela ou exibição na exibição de fonte de dados.|  
|[Relações de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)|Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], atributos dentro de uma dimensão sempre são relacionados direta ou indiretamente ao atributo de chave. Quando você define uma dimensão com base em um esquema em estrela, onde todos os atributos de dimensão são derivados da mesma tabela relacional, uma relação de atributo é automaticamente definida entre o atributo de chave e cada atributo não chave da dimensão. Quando você define uma dimensão com base em um esquema de floco de neve, onde todos os atributos de dimensão derivam de várias tabelas relacionadas, uma relação de atributo é automaticamente definida da seguinte maneira:<br /><br /> Entre o atributo de chave e cada atributo não chave vinculado às colunas na tabela de dimensões principal.<br /><br /> Entre o atributo de chave e atributo vinculado à chave estrangeira na tabela secundária que vincula as tabelas de dimensões subjacentes.<br /><br /> Entre o atributo vinculado à chave estrangeira na tabela secundária e cada atributo não chave vinculado às colunas da tabela secundária.|  
  
  
