---
title: Assistente de geração de esquema (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- relational schema [Analysis Services]
ms.assetid: 68bf7ba3-d0cb-437f-9a3e-9edc0999af19
author: minewiskan
ms.author: owend
ms.openlocfilehash: 513873fdf808ff62058ad765983cb1ebd512cd2d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545693"
---
# <a name="schema-generation-wizard-analysis-services"></a>Assistente de Geração de Esquema (Analysis Services)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oferece suporte a dois métodos de trabalho com esquemas relacionais ao definir objetos OLAP em um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Geralmente, você define objetos OLAP com base em um modelo de dados lógico construído em uma exibição da fonte de dados de um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Essa exibição da fonte de dados é definida com base nos elementos do esquema de uma ou mais fontes de dados relacionais, conforme personalizado na exibição da fonte de dados.  
  
 Como alternativa, você pode definir objetos OLAP primeiro e, em seguida, gerar uma exibição da fonte de dados, uma fonte de dados e o esquema de banco de dados relacional subjacente que dá suporte a estes objetos OLAP. Esse banco de dados relacional é chamado banco de dados da área de assunto.  
  
 Essa abordagem é chamada às vezes de design hierárquico e é usado com frequência na criação de protótipos e modelagem de análise. Quando você usar esta abordagem, usará o Assistente de Geração de Esquema para criar a exibição de fonte de dados subjacente e os objetos de fonte de dados baseados nos objetos OLAP definidos em um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Esta é uma abordagem iterativa. Você provavelmente executará novamente o assistente várias vezes à medida que altera o design das dimensões e dos cubos. Cada vez que você executar o assistente, ele incorporará as alterações aos objetos subjacentes e, na medida do possível, preservará os dados contidos nos bancos de dados subjacentes.  
  
 O esquema gerado é um esquema de mecanismo de banco de dados relacional SQL Server. O assistente não gera esquemas para outros produtos de banco de dados relacional.  
  
 Os dados que são populados no banco de dados de área de assunto são adicionados separadamente, usando quaisquer ferramentas e técnicas que você usa para popular um banco de dados relacional SQL Server. Na maioria dos casos, os dados são preservados quando você executa novamente o assistente, mas há exceções. Por exemplo, alguns dados devem ser descartados se você excluir uma dimensão ou um atributo que contêm dados. Se o Assistente de Geração de Esquema tiver que descartar alguns dados devido a uma alteração no esquema, você receberá um aviso de que os dados serão descartados e poderá cancelar a nova geração.  
  
 Como regra geral, qualquer alteração que você fizer em um objeto que foi gerado originalmente pelo Assistente de Geração de Esquema será substituída quando o Assistente de Geração de Esquema gerar esse objeto novamente na sequência. A exceção primordial a essa regra é quando você adiciona colunas a uma tabela que o Assistente de Geração de Esquema gerou. Nesse caso, o Assistente de Geração de Esquema preservará as colunas que você adicionou à tabela, bem como seus dados.  
  
## <a name="in-this-section"></a>Nesta seção  
 A tabela a seguir lista os tópicos adicionais que explicam como trabalhar com o Assistente de Geração de Esquema.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Use o assistente de geração de esquema &#40;Analysis Services&#41;](schema-generation-wizard-analysis-services.md)|Descreve como gerar o esquema para a área de assunto e os bancos de dados da área de preparação.|  
|[Entendendo os esquemas de banco de dados](understanding-the-database-schemas.md)|Descreve o esquema gerado para a área de assunto e os bancos de dados da área de preparação.|  
|[Entendendo a geração com incremento](understanding-incremental-generation.md)|Descreve os recursos de geração incremental do Assistente de Geração de Esquema.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições da fonte de dados em modelos multidimensionais](data-source-views-in-multidimensional-models.md)   
 [Fontes de dados em modelos multidimensionais](data-sources-in-multidimensional-models.md)   
 [Fontes de dados com suporte &#40;SSAS multidimensional&#41;](supported-data-sources-ssas-multidimensional.md)  
  
  
