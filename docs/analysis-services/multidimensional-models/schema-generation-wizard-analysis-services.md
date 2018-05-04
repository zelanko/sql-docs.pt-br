---
title: Assistente de geração de esquema (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 653e28218cf7a89a7a8b4fae7735b16d3b875f61
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="schema-generation-wizard-analysis-services"></a>Assistente de Geração de Esquema (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oferece suporte a dois métodos de trabalho com esquemas relacionais ao definir objetos OLAP em um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Geralmente, você define objetos OLAP com base em um modelo de dados lógico construído em uma exibição da fonte de dados de um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Essa exibição da fonte de dados é definida com base nos elementos do esquema de uma ou mais fontes de dados relacionais, conforme personalizado na exibição da fonte de dados.  
  
 Como alternativa, você pode definir objetos OLAP primeiro e, em seguida, gerar uma exibição da fonte de dados, uma fonte de dados e o esquema de banco de dados relacional subjacente que dá suporte a estes objetos OLAP. Esse banco de dados relacional é chamado banco de dados da área de assunto.  
  
 Essa abordagem é chamada às vezes de design hierárquico e é usado com frequência na criação de protótipos e modelagem de análise. Quando você usar esta abordagem, usará o Assistente de Geração de Esquema para criar a exibição de fonte de dados subjacente e os objetos de fonte de dados baseados nos objetos OLAP definidos em um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Esta é uma abordagem iterativa. Você provavelmente executará novamente o assistente várias vezes à medida que altera o design das dimensões e dos cubos. Cada vez que você executar o assistente, ele incorporará as alterações aos objetos subjacentes e, na medida do possível, preservará os dados contidos nos bancos de dados subjacentes.  
  
 O esquema gerado é um esquema de mecanismo de banco de dados relacional SQL Server. O assistente não gera esquemas para outros produtos de banco de dados relacional.  
  
 Os dados que são populados no banco de dados de área de assunto são adicionados separadamente, usando quaisquer ferramentas e técnicas que você usa para popular um banco de dados relacional SQL Server. Na maioria dos casos, os dados são preservados quando você executa novamente o assistente, mas há exceções. Por exemplo, alguns dados devem ser descartados se você excluir uma dimensão ou um atributo que contêm dados. Se o Assistente de Geração de Esquema tiver que descartar alguns dados devido a uma alteração no esquema, você receberá um aviso de que os dados serão descartados e poderá cancelar a nova geração.  
  
 Como regra geral, qualquer alteração que você fizer em um objeto que foi gerado originalmente pelo Assistente de Geração de Esquema será substituída quando o Assistente de Geração de Esquema gerar esse objeto novamente na sequência. A exceção primordial a essa regra é quando você adiciona colunas a uma tabela que o Assistente de Geração de Esquema gerou. Nesse caso, o Assistente de Geração de Esquema preservará as colunas que você adicionou à tabela, bem como seus dados.  
  
## <a name="in-this-section"></a>Nesta seção  
 A tabela a seguir lista os tópicos adicionais que explicam como trabalhar com o Assistente de Geração de Esquema.  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Use o assistente de geração de esquema &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/use-the-schema-generation-wizard-analysis-services.md)|Descreve como gerar o esquema para a área de assunto e os bancos de dados da área de preparação.|  
|[Entendendo os esquemas de banco de dados](../../analysis-services/multidimensional-models/understanding-the-database-schemas.md)|Descreve o esquema gerado para a área de assunto e os bancos de dados da área de preparação.|  
|[Entendendo a geração com incremento](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)|Descreve os recursos de geração incremental do Assistente de Geração de Esquema.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições da fonte de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Fontes de dados com suporte &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
