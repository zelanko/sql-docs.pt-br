---
title: Dimensões em modelos multidimensionais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OLAP [Analysis Services], dimensions
- dimensions [Analysis Services], about dimensions
- OLAP objects [Analysis Services], dimensions
ms.assetid: 2b62b05c-00fd-4e60-b77f-f707ba83a19b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 520d6f11e5a472d5337a3747cc73c1d3656171c2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075174"
---
# <a name="dimensions-in-multidimensional-models"></a>Dimensões em modelos multidimensionais
  Uma dimensão do banco de dados é uma coleção de objetos relacionados, chamados atributos, que podem ser usados para fornecer informações sobre dados de fatos de um ou mais cubos. Por exemplo, seriam atributos comuns de uma dimensão de produto o nome do produto, sua categoria, linha de produtos, tamanho e preço. Esses objetos são vinculados a uma ou mais colunas de uma ou mais tabelas de uma exibição da fonte de dados. Por padrão, esses atributos são visíveis como hierarquias de atributo e podem ser usados no entendimento dos dados de fatos de um cubo. Os atributos podem ser organizados em hierarquias definidas pelo usuário que fornecem os caminhos de navegação para ajudar os usuários durante pesquisas dos dados de um cubo.  
  
 Os cubos contêm todas as dimensões que servem de base para os usuários realizarem análises dos dados de fatos. Uma instância de uma dimensão do banco de dados de um cubo é chamada dimensão do cubo e se relaciona a um ou mais grupos de medidas do cubo. Uma dimensão do banco de dados pode ser usada várias vezes em um cubo. Por exemplo, uma tabela de fatos pode ter diversos fatos relacionados ao tempo, sendo possível definir uma dimensão de cubo separada para auxiliar na análise de cada um deles. No entanto, é preciso haver apenas uma dimensão do banco de dados relacionada ao tempo, ou seja, também é necessário que haja somente uma tabela do banco de dados relacional associada ao tempo para oferecer suporte a várias dimensões do cubo baseadas no tempo.  
  
> [!NOTE]  
>  Para obter informações sobre questões de desempenho relacionadas ao design da dimensão, consulte o [SQL Server 2008 R2 Analysis Services Performance Guide](https://go.microsoft.com/fwlink/?LinkId=306717).  
  
## <a name="defining-dimensions-attributes-and-hierarchies"></a>Definindo dimensões, atributos e hierarquias.  
 O método mais simples para definir dimensões, atributos e hierarquias de bancos de dados e cubos é usar o Assistente para Cubos para criar as dimensões ao mesmo tempo em que você define o cubo. O Assistente para Cubos criará dimensões com base nas tabelas de dimensões da exibição da fonte de dados que o assistente identificar ou que você especificar para uso no cubo. O assistente então criará as dimensões do banco de dados e as adicionará ao novo cubo, criando as dimensões do cubo.  
  
 Ao criar um cubo, você também pode adicionar a ele todas as dimensões já existentes no banco de dados. Elas podem ter sido previamente definidas para outro cubo ou pelo Assistente para Dimensões. Depois que a dimensão do banco de dados estiver definida, será possível modificá-la e configurá-la no Designer de Dimensão. Até um certo limite, você também pode personalizar a dimensão do cubo no Designer de Cubo.  
  
> [!NOTE]  
>  Também é possível projetar e configurar dimensões, atributos e hierarquias de forma programática usando o XMLA ou o Analysis Management Objects (AMO). Para obter mais informações, consulte [Analysis Services linguagem de script &#40;ASSL&#41; referência](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla) e [desenvolvimento com Objetos de Gerenciamento de Análise &#40;amo&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).  
  
## <a name="in-this-section"></a>Nesta seção  
 A tabela a seguir descreve os tópicos dessa seção.  
  
 [Definir as dimensões do banco de dados](define-database-dimensions.md)  
 Descreve como modificar e configurar uma dimensão do banco de dados usando o Designer de Dimensão.  
  
 [Referência de propriedades de atributo de dimensão](dimension-attribute-properties-reference.md)  
 Descreve como definir, modificar e configurar um atributo da dimensão do banco de dados usando o Designer de Dimensão.  
  
 [Definir relações de atributo](attribute-relationships-define.md)  
 Descreve como definir, modificar e configurar uma relação de atributos usando o Designer de Dimensão.  
  
 [Criar hierarquias definidas pelo usuário](user-defined-hierarchies-create.md)  
 Descreve como definir, modificar e configurar uma hierarquia definida pelo usuário de atributos da dimensão usando o Designer de Dimensão.  
  
 [Usar o Assistente de Business Intelligence para aprimorar dimensões](../use-the-business-intelligence-wizard-to-enhance-dimensions.md)  
 Descreve como aprimorar a dimensão do banco de dados usando o Assistente de Business Intelligence.  
  
## <a name="see-also"></a>Consulte Também  
 [Cubos em modelos multidimensionais](cubes-in-multidimensional-models.md)  
  
  
