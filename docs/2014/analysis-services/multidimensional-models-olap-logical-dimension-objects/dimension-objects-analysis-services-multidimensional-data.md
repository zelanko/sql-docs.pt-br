---
title: Objetos (Analysis Services - dados multidimensionais) de dimensão | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], objects
ms.assetid: 7f3d55c7-cccb-4ad0-b6cb-3a2c9992dd68
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 415cbc4527d21e6bd14945bf911bb6d6a67f5e38
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249416"
---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>Objetos de dimensão (Analysis Services - Dados Multidimensionais)
  Um simples objeto <xref:Microsoft.AnalysisServices.Dimension> é composto de: informações básicas, atributos e hierarquias. As informações básicas incluem o nome da dimensão, o tipo de dimensão, a fonte de dados, o modo de armazenamento e outros. Os atributos definem os dados reais na dimensão. Os atributos não necessariamente pertencem a uma hierarquia, mas hierarquias são criadas a partir de atributos. Uma hierarquia cria listas ordenadas de níveis e define os modos como um usuário pode explorar a dimensão.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir fornecem mais informações sobre como projetar e implementar objetos de dimensão.  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Dimensões &#40;Analysis Services - dados multidimensionais&#41;](dimensions-analysis-services-multidimensional-data.md)|Na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], as dimensões são um componente fundamental dos cubos. As dimensões organizam dados com relação a uma área de interesse, como clientes, lojas ou funcionários, para usuários.|  
|[Atributos e hierarquias de atributos](attributes-and-attribute-hierarchies.md)|As dimensões são coleções de atributos, vinculados a uma ou mais colunas na tabela ou exibição na exibição de fonte de dados.|  
|[Relações de atributo](attribute-relationships.md)|Na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], atributos dentro de uma dimensão sempre estão relacionados diretamente ou indiretamente ao atributo de chave. Quando você define uma dimensão com base em um esquema em estrela, onde todos os atributos de dimensão são derivados da mesma tabela relacional, uma relação de atributo é automaticamente definida entre o atributo de chave e cada atributo não chave da dimensão. Quando você define uma dimensão com base em um esquema de floco de neve, onde todos os atributos de dimensão derivam de várias tabelas relacionadas, uma relação de atributo é automaticamente definida da seguinte maneira:<br /><br /> -Entre o atributo de chave e cada não-chave atributo associado a colunas na tabela de dimensões principal.<br />-Entre o atributo de chave e o atributo associado à chave estrangeira na tabela secundária que vincula as tabelas de dimensões subjacente.<br />-Entre o atributo vinculado à chave estrangeira na tabela secundária e cada atributo não chave vinculado às colunas da tabela secundária.|  
  
  
