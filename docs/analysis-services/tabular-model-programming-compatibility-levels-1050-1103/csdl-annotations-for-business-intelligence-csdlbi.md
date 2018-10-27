---
title: Anotações CSDL para Business Intelligence (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3eac4057f8a4db818a02068f33cbc7b295353f0c
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145861"
---
# <a name="csdl-annotations-for-business-intelligence-csdlbi"></a>CSDLBI (Anotações CSDL para Business Intelligence)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte à apresentação da definição de um modelo de tabela em um formato XML chamado CSDLBI (Linguagem de Definição de Esquema Conceitual com anotações de Business Intelligence). Este tópico fornece uma visão geral da CSDLBI e como ela é usada com os modelos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="understanding-the-role-of-csdl"></a>Compreendendo a função da CSDL  
 A CSDL (Linguagem de Definição de Esquema Conceitual) é uma linguagem em XML que descreve entidades, relações e funções. A CSDL é definida como parte da Estrutura de Dados de Entidade. As anotações de BI são uma extensão criada para oferecer suporte à modelagem de dados usando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Embora a CSDL seja compatível com a Estrutura de Dados de Entidade, não é necessário compreender o modelo de relação entre entidades nem ter ferramentas especiais para criar um modelo de tabela ou um relatório baseado em um modelo. Você cria modelos usando ferramentas de cliente, como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], ou uma API, como AMO, e implanta o modelo em um servidor.  
  
 Um esquema da CSDL é gerado pelo servidor do Analysis Services em resposta a uma solicitação por uma definição de modelo de um cliente, como o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. O aplicativo cliente envia uma consulta XML ao servidor do Analysis Services que hospeda os dados modelo. Em resposta, o servidor envia uma mensagem XML que contém uma definição das entidades no modelo, usando as anotações da CSDLBI. O cliente de relatórios usa as informações para apresentar os campos, as agregações e as medidas disponíveis no modelo. As anotações da CSDL também fornecem informações sobre como agrupar, classificar e formatar os dados.  
  
 Para obter informações gerais sobre a CSDLBI, consulte [conceitos da CSDLBI](https://docs.microsoft.com/bi-reference/csdl/csdlbi-concepts).  
  
### <a name="working-with-csdl"></a>Trabalhando com a CSDL  
 O conjunto de anotações da CSDLBI que representa qualquer modelo de tabela específico é um documento XML que contém uma coleção de entidades, simples e complexas. As entidades definem tabelas (ou dimensões), colunas (atributos), associações (relações) e fórmulas incluídas em colunas calculadas, medidas ou KPIs.  
  
 Você não pode modificar estes objetos diretamente, mas deve usar as ferramentas de cliente e APIs (interfaces de programação de aplicativo) fornecidas para trabalhar com modelos de tabela.  
  
 Você pode obter a CSDL para um modelo enviando uma solicitação DISCOVER ao servidor que hospeda o modelo. A solicitação deve ser qualificada especificando o servidor e o modelo e, opcionalmente, uma exibição ou perspectiva. A mensagem retornada é uma cadeia de caracteres XML. Certos elementos dependem da linguagem e retornam valores diferentes de acordo com a linguagem da conexão atual. Para obter mais informações, consulte [conjunto de linhas DISCOVER_CSDL_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset).  
  
### <a name="csdlbi-versions"></a>Versões da CSDLBI  
 A especificação da CSDL original (da Estrutura de Dados de Entidade) oferece a maioria das entidades e propriedades necessárias para oferecer suporte à modelagem. As anotações de BI oferecem suporte aos requisitos especiais de modelos de tabela, às propriedades de relatório exigidas por clientes como o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] e aos metadados adicionais exigidos pelos modelos multidimensionais. Esta seção descreve as atualizações em cada versão.  
  
 **1.0 DA CSDLBI**  
  
 O conjunto inicial de adições ao esquema da CSDL para oferecer suporte a modelos de tabela do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] continha anotações para suporte à modelagem de dados, aos cálculos personalizados e à apresentação aprimorada:  
  
-   Novos elementos e propriedades para oferecer suporte a modelos de tabela. Por exemplo, uma propriedade foi adicionada para especificar o tipo de consulta de banco de dados usado para popular o modelo.  
  
-   Novas propriedades e extensões para entidades existentes.  Por exemplo, o elemento Association foi estendido para oferecer suporte a relações.  
  
-   Propriedades de visualização e navegação. Por exemplo, as propriedades foram adicionadas para oferecer suporte a campos de classificação personalizados, imagens padrão e  
  
 **1.1 DA CSDLBI**  
  
 Essa versão do esquema da CSDLBI inclui adições para suporte de bancos de dados multidimensionais (como cubos OLAP). Os novos elementos e propriedades são os seguintes:  
  
-   Suporte para dimensões como entidades.  
  
-   Suporte para hierarquias.  
  
-   Exposição de partições ROLAP.  
  
-   Suporte para traduções.  
  
-   Suporte para perspectivas.  
  
 Para obter informações detalhadas sobre os elementos individuais nas anotações da CSDLBI, consulte [referência técnica para anotações de BI para CSDL](https://docs.microsoft.com/bi-reference/csdl/technical-reference-for-bi-annotations-to-csdl). Para obter informações sobre a especificação principal de CSDL, consulte o [especificação de CSDL](http://go.microsoft.com/fwlink/?LinkId=205855) no MSDN.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre o modelo de objeto Tabular em compatibilidade níveis 1050 até 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Conceitos da CSDLBI](https://docs.microsoft.com/bi-reference/csdl/csdlbi-concepts)   
 [Noções básicas sobre o modelo de objeto Tabular em compatibilidade níveis 1050 até 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
