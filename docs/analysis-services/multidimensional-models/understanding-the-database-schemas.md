---
title: Entendendo os esquemas de banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Schema Generation Wizard, database schema
- database schema [Analysis Services]
- relational schema [Analysis Services], database schema
- subject area schema options [Analysis Services]
- staging area schema options [Analysis Services]
- denormalized schemas
ms.assetid: 51e411f9-ee3f-4b92-9833-c2bce8c6b752
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 12d62289fe08395c91eff39202b60ee0f67ff82a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="understanding-the-database-schemas"></a>Entendendo os esquemas de banco de dados
  O Assistente de Geração de Esquema gera um esquema relacional não normalizado para o banco de dados da área de assunto com base nas dimensões e nos grupos de medidas do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O assistente gera uma tabela relacional para cada dimensão para armazenar dados da dimensão, chamada tabela de dimensões, e uma tabela relacional para cada grupo de medidas para armazenar dados de fatos, chamada tabela de fatos. O assistente ignora dimensões vinculadas, grupos de medidas vinculados e dimensões de tempo de servidor ao gerar essas tabelas relacionais.  
  
## <a name="validation"></a>Validação  
 Antes de começar a gerar o esquema relacional subjacente, o Assistente de Geração de Esquema valida os cubos e dimensões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se detectar erros, o assistente parará e os reportará na janela Lista de Tarefas do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. São exemplos de erros que impedem a geração:  
  
-   Dimensões com mais de um atributo de chave.  
  
-   Atributos pai com tipos de dados diferentes dos atributos de chave.  
  
-   Grupos de medidas sem-medidas.  
  
-   Dimensões de degeneração ou medidas configuradas incorretamente.  
  
-   Chaves substitutas configuradas incorretamente, como vários atributos usando o tipo de atributo **ScdOriginalID** ou um atributo usando **ScdOriginalID** que não está associado a uma coluna que usa o tipo de dados de número inteiro.  
  
## <a name="dimension-tables"></a>Tabelas de dimensões  
 Para cada dimensão, o Assistente de Geração de Esquema gera uma tabela de dimensões que será incluída no banco de dados da área de assunto. A estrutura da tabela de dimensões varia de acordo com as escolhas feitas durante a criação da dimensão na qual ela se baseia.  
  
 Colunas  
 O assistente gera uma coluna para ligações associadas a cada atributo da dimensão na qual a tabela de dimensões baseia-se, como as ligações para as propriedades **KeyColumns**, **NameColumn**, **ValueColumn**, **CustomRollupColumn**, **CustomRollupPropertiesColumn**e **UnaryOperatorColumn** de cada atributo.  
  
 Relações  
 O assistente gera uma relação entre a coluna de cada atributo e a chave primária da tabela de dimensões.  
  
 O assistente também gera uma relação entre a chave primária de cada tabela de dimensões adicional definida como dimensão de referência no cubo, se aplicável.  
  
 Restrições  
 Por padrão, o assistente gera uma restrição de chave primária para cada tabela de dimensões com base no atributo de chave da dimensão. Se a restrição de chave primária for gerada, uma coluna de nome separada será gerada por padrão. A chave primária lógica será criada na exibição da fonte de dados mesmo que você decida não criar a chave primária no banco de dados.  
  
> [!NOTE]  
>  Ocorrerá um erro se mais de uma atributo de chave for especificado na dimensão na qual se baseia a tabela de dimensões.  
  
 Traduções  
 O assistente gera uma tabela separada para manter os valores traduzidos para qualquer atributo que precise de uma coluna de tradução. O assistente cria também uma coluna separada para cada um dos idiomas necessários.  
  
## <a name="fact-tables"></a>Tabelas de fatos  
 Para cada grupo de medidas de um cubo, o Assistente de Geração de Esquema gera uma tabela de fatos que será incluída no banco de dados de área de assunto. A estrutura da tabela de fatos varia de acordo com as escolhas feitas durante a criação do grupo de medidas no qual ela se baseia e as relações estabelecidas entre o grupo de medidas e as dimensões incluídas.  
  
 Colunas  
 O assistente gera uma coluna para cada medida, exceto para medidas que usam a função de agregação **Count** . Essas medidas não requerem uma coluna correspondente na tabela de fatos.  
  
 O assistente gera também uma coluna para cada coluna de atributo de granularidade de cada relação de dimensão regular do grupo de medidas e uma ou mais colunas para as ligações associadas a cada atributo de uma dimensão que contém uma relação de dimensão de fatos com o grupo de medidas que serve de base para a tabela, se aplicável.  
  
 Relações  
 O assistente gera uma relação para cada relação de dimensão regular entre a tabela de fatos e o atributo de granularidade da tabela de dimensões. Se a granularidade for baseada no atributo de chave da tabela de dimensões, a relação será criada no banco de dados e na exibição da fonte de dados. Se a granularidade for baseada em outro atributo, a relação será criada apenas na exibição da fonte de dados.  
  
 Se você decidir gerar índices pelo assistente, um índice não cluster será gerado para cada uma dessas colunas de relação.  
  
 Restrições  
 Não são geradas chaves primárias em tabelas de fatos.  
  
 Se você decidir impor a integridade referencial, restrições de integridade referencial serão geradas entre as tabelas de dimensões e as tabelas de fatos sempre que aplicável.  
  
 Traduções  
 O assistente gera uma tabela separada para manter os valores traduzidos para qualquer propriedade do grupo de medidas que precise de uma coluna de tradução. O assistente cria também uma coluna separada para cada um dos idiomas necessários.  
  
## <a name="data-type-conversion-and-default-lengths"></a>Conversão do tipo de dados e comprimentos padrão  
 O Assistente de Geração de Esquema sempre ignora os tipos de dados, exceto no caso de colunas que usam o tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **wchar** data type. O tamanho de dados **wchar** converte-se diretamente no tipo de dados **nvarchar** . No entanto, se o comprimento especificado de uma coluna que usa o tamanho **wchar** for superior a 4000 bytes, o Assistente de Geração de Esquema produzirá um erro.  
  
 Se um item de dados, como uma ligação para um atributo, não tiver um comprimento especificado, o comprimento padrão listado na tabela a seguir será usado na coluna.  
  
|Item de dados|Comprimento padrão (bytes)|  
|---------------|------------------------------|  
|KeyColumn|50|  
|NameColumn|50|  
|CustomRollupColumn|3000|  
|CustomRollupPropertiesColumn|500|  
|UnaryOperatorColumn|1|  
  
## <a name="see-also"></a>Consulte também  
 [Entendendo a geração com incremento](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)   
 [Gerenciar alterações em exibições da fonte de dados e fontes de dados](../../analysis-services/multidimensional-models/manage-changes-to-data-source-views-and-data-sources.md)  
  
  
