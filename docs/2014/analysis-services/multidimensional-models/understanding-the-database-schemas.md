---
title: Noções básicas sobre os esquemas de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema Generation Wizard, database schema
- database schema [Analysis Services]
- relational schema [Analysis Services], database schema
- subject area schema options [Analysis Services]
- staging area schema options [Analysis Services]
- denormalized schemas
ms.assetid: 51e411f9-ee3f-4b92-9833-c2bce8c6b752
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef75cf2773781f94bd02a26c5c94958b9f4dfe3f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282242"
---
# <a name="understanding-the-database-schemas"></a>Entendendo os esquemas de banco de dados
  O Assistente de Geração de Esquema gera um esquema relacional não normalizado para o banco de dados da área de assunto com base nas dimensões e nos grupos de medidas do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O assistente gera uma tabela relacional para cada dimensão para armazenar dados da dimensão, chamada tabela de dimensões, e uma tabela relacional para cada grupo de medidas para armazenar dados de fatos, chamada tabela de fatos. O assistente ignora dimensões vinculadas, grupos de medidas vinculados e dimensões de tempo de servidor ao gerar essas tabelas relacionais.  
  
## <a name="validation"></a>Validação  
 Antes de começar a gerar o esquema relacional subjacente, o Assistente de Geração de Esquema valida os cubos e dimensões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se detectar erros, o assistente parará e os reportará na janela Lista de Tarefas do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. São exemplos de erros que impedem a geração:  
  
-   Dimensões com mais de um atributo de chave.  
  
-   Atributos pai com tipos de dados diferentes dos atributos de chave.  
  
-   Grupos de medidas sem-medidas.  
  
-   Dimensões de degeneração ou medidas configuradas incorretamente.  
  
-   Chaves substitutas configuradas incorretamente, como vários atributos usando o tipo de atributo `ScdOriginalID` ou um atributo usando `ScdOriginalID` que não está associado a uma coluna que usa o tipo de dados de número inteiro.  
  
## <a name="dimension-tables"></a>Tabelas de dimensões  
 Para cada dimensão, o Assistente de Geração de Esquema gera uma tabela de dimensões que será incluída no banco de dados da área de assunto. A estrutura da tabela de dimensões varia de acordo com as escolhas feitas durante a criação da dimensão na qual ela se baseia.  
  
 Colunas  
 O assistente gera uma coluna para ligações associadas a cada atributo na dimensão na qual a tabela de dimensões baseia-se, como as ligações para o `KeyColumns`, `NameColumn`, `ValueColumn`, `CustomRollupColumn`, `CustomRollupPropertiesColumn`e `UnaryOperatorColumn`propriedades de cada atributo.  
  
 Relações  
 O assistente gera uma relação entre a coluna de cada atributo e a chave primária da tabela de dimensões.  
  
 O assistente também gera uma relação entre a chave primária de cada tabela de dimensões adicional definida como dimensão de referência no cubo, se aplicável.  
  
 Restrições  
 Por padrão, o assistente gera uma restrição de chave primária para cada tabela de dimensões com base no atributo de chave da dimensão. Se a restrição de chave primária for gerada, uma coluna de nome separada será gerada por padrão. A chave primária lógica será criada na exibição da fonte de dados mesmo que você decida não criar a chave primária no banco de dados.  
  
> [!NOTE]  
>  Ocorrerá um erro se mais de uma atributo de chave for especificado na dimensão na qual se baseia a tabela de dimensões.  
  
 Translations  
 O assistente gera uma tabela separada para manter os valores traduzidos para qualquer atributo que precise de uma coluna de tradução. O assistente cria também uma coluna separada para cada um dos idiomas necessários.  
  
## <a name="fact-tables"></a>Tabelas de fatos  
 Para cada grupo de medidas de um cubo, o Assistente de Geração de Esquema gera uma tabela de fatos que será incluída no banco de dados de área de assunto. A estrutura da tabela de fatos varia de acordo com as escolhas feitas durante a criação do grupo de medidas no qual ela se baseia e as relações estabelecidas entre o grupo de medidas e as dimensões incluídas.  
  
 Colunas  
 O assistente gera uma coluna para cada medida, exceto para medidas que usam o `Count` função de agregação. Essas medidas não requerem uma coluna correspondente na tabela de fatos.  
  
 O assistente gera também uma coluna para cada coluna de atributo de granularidade de cada relação de dimensão regular do grupo de medidas e uma ou mais colunas para as ligações associadas a cada atributo de uma dimensão que contém uma relação de dimensão de fatos com o grupo de medidas que serve de base para a tabela, se aplicável.  
  
 Relações  
 O assistente gera uma relação para cada relação de dimensão regular entre a tabela de fatos e o atributo de granularidade da tabela de dimensões. Se a granularidade for baseada no atributo de chave da tabela de dimensões, a relação será criada no banco de dados e na exibição da fonte de dados. Se a granularidade for baseada em outro atributo, a relação será criada apenas na exibição da fonte de dados.  
  
 Se você decidir gerar índices pelo assistente, um índice não cluster será gerado para cada uma dessas colunas de relação.  
  
 Restrições  
 Não são geradas chaves primárias em tabelas de fatos.  
  
 Se você decidir impor a integridade referencial, restrições de integridade referencial serão geradas entre as tabelas de dimensões e as tabelas de fatos sempre que aplicável.  
  
 Translations  
 O assistente gera uma tabela separada para manter os valores traduzidos para qualquer propriedade do grupo de medidas que precise de uma coluna de tradução. O assistente cria também uma coluna separada para cada um dos idiomas necessários.  
  
## <a name="data-type-conversion-and-default-lengths"></a>Conversão do tipo de dados e comprimentos padrão  
 Assistente de geração de esquema sempre ignora os tipos de dados em todos os casos, exceto nas colunas que usam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `wchar` tipo de dados. O `wchar` tamanho de dados se traduz diretamente para o `nvarchar` tipo de dados. No entanto, se o comprimento especificado de uma coluna que usa o tamanho `wchar` for superior a 4000 bytes, o Assistente de Geração de Esquema produzirá um erro.  
  
 Se um item de dados, como uma ligação para um atributo, não tiver um comprimento especificado, o comprimento padrão listado na tabela a seguir será usado na coluna.  
  
|Item de dados|Comprimento padrão (bytes)|  
|---------------|------------------------------|  
|KeyColumn|50|  
|NameColumn|50|  
|CustomRollupColumn|3000|  
|CustomRollupPropertiesColumn|500|  
|UnaryOperatorColumn|1|  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre geração Incremental](understanding-incremental-generation.md)   
 [Gerenciar alterações em exibições da fonte de dados e em fontes de dados](manage-changes-to-data-source-views-and-data-sources.md)  
  
  
