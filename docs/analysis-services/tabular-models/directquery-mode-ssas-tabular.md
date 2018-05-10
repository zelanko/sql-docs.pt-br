---
title: O modo DirectQuery | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a5ee42a6e29a22ddc68d4ff10714a6d66e28a26
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
---
# <a name="directquery-mode"></a>Modo DirectQuery
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve *o modo DirectQuery* para modelos de tabela do Analysis Services nos níveis de compatibilidade 1200 e superior. O modo DirectQuery pode ser ativado para modelos que estão sendo criados no SSDT; para modelos de tabela que já foram implantados, você pode alterar para o modo DirectQuery no SSMS. Antes de escolher o modo DirectQuery, é importante entender os benefícios e as restrições.
  
##  <a name="bkmk_Benefits"></a> Benefícios
 Por padrão, modelos de tabela usam um cache na memória para armazenar e consultar dados. Quando os modelos de tabela usam dados de consulta que residem na memória, até mesmo consultas complexas podem ser inacreditavelmente rápidas. No entanto, há algumas limitações no uso de dados armazenados em cache. São elas: grandes conjuntos de dados podem exceder a memória disponível, e pode ser difícil, se não impossível, atender aos requisitos de atualização dos dados em uma agenda regular de processamento.  
  
 O DirectQuery supera essas limitações, ao mesmo tempo que aproveita os recursos RDBMS, tornando a execução da consulta mais eficiente. Com o DirectQuery:  
  
-   Os dados estão atualizados e não há sobrecarga de gerenciamento adicional pela manutenção de uma cópia separada dos dados (o cache na memória). As alterações nos dados de origem subjacentes podem ser refletidas imediatamente em consultas no modelo de dados.  
  
-   Os conjuntos de dados podem ser maiores do que a capacidade de memória de um servidor do Analysis Services.  
  
-   DirectQuery pode tirar proveito de aceleração de consulta do provedor, como a fornecida por índices de coluna de otimização de memória.  
  
-   A segurança pode ser imposta pelo banco de dados de back-end, usando recursos de segurança em nível de linha do banco de dados (como alternativa, você pode usar a segurança em nível de linha no modelo por meio do DAX).  
  
-   Se o modelo contiver fórmulas complexas que possam exigir várias consultas, o Analysis Services poderá executar a otimização para garantir que o plano de consulta da consulta executado no banco de dados back-end seja o mais eficiente possível.  
  
##  <a name="bkmk_prereq"></a>Restrições
Os modelos de tabela no modo DirectQuery apresentam algumas restrições. Antes de mudar os modos, é importante determinar se as vantagens da execução da consulta no servidor back-end superam qualquer redução na funcionalidade.  
  
 Se você alterar o modo de um modelo existente no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], o designer do modelo notificará você sobre qualquer recurso em seu modelo que seja incompatível com o modo DirectQuery.  
  
 A seguinte lista resume as principais restrições de recursos a serem consideradas:  
  
|||  
|-|-|  
|**Área do recurso**|**Restrição**|  
|**Fontes de Dados**|Os modelos do DirectQuery só podem usar dados de um banco de dados relacional dos seguintes tipos: SQL Server, Banco de Dados SQL do Azure, Oracle e Teradata.  Consulte Fontes de dados com suporte no DirectQuery adiante neste artigo para obter informações de versão e de provedor.| 
|**Procedimentos armazenados do SQL**|Para modelos do DirectQuery, os procedimentos armazenados não podem ser especificados em uma instrução SQL para definir as tabelas ao usar o Assistente de Importação de Dados. |   
|**Tabelas calculadas**|As tabelas calculadas não têm suporte para modelos DirectQuery, mas as colunas calculadas têm. Se você tentar converter um modelo de tabela que contém uma tabela calculada, ocorrerá um erro informando que o modelo não pode conter dados colados.|  
|**Limites de consulta**|O limite de linha padrão é um milhão de linhas, que você pode aumentar especificando **MaxIntermediateRowSize** no arquivo msmdsrv.ini. Consulte [Propriedades do DAX](../../analysis-services/server-properties/dax-properties.md) para obter detalhes.
|**Fórmulas DAX**|Ao consultar um modelo de tabela no modo DirectQuery, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] converte todas as fórmulas DAX e definições de medida em instruções SQL. As fórmulas DAX que contêm elementos que não podem ser convertidos em sintaxe SQL retornarão erros de validação no modelo.<br /><br /> Na maioria das vezes, essa restrição é limitada a algumas funções DAX. Para medidas, as fórmulas DAX são convertidas em operações baseadas em conjunto no repositório de dados relacional. Isso significa que todas as medidas criadas implicitamente têm suporte. <br /><br /> Quando ocorrer um erro de validação, você precisará gravar a fórmula novamente, substituindo uma função diferente, ou encontrar uma solução alternativa para isso usando colunas derivadas na fonte de dados.  Se um modelo de tabela incluir fórmulas que contêm funções incompatível, isso será relatado quando você mudar para o modo DirectQuery no designer. <br /><br />**Observação:**  algumas fórmulas no modelo podem ser validadas quando você muda o modelo para o modo DirectQuery, mas retornam resultados diferentes quando executadas no cache versus no armazenamento de dados relacionais. Isso ocorre porque os cálculos no cache usam a semântica do mecanismo de análise na memória (que contém recursos que visam emular o comportamento do Excel), enquanto as consultas nos dados armazenados na fonte de dados relacionais usam a semântica do SQL Server.<br /><br /> SQL armazenado  <br /><br /> Para obter mais informações, consulte [compatibilidade de fórmula do DAX no modo DirectQuery](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md).|  
|**Consistência de fórmula**|Em alguns casos, a mesma fórmula pode retornar resultados diferentes em um modelo em cache comparado a um modelo do DirectQuery que usa apenas o armazenamento de dados relacionais. Estas diferenças são uma consequência das diferenças semânticas entre o mecanismo de análise in-memory e o SQL Server.<br /><br /> Para obter uma lista completa de problemas de compatibilidade, incluindo funções que podem retornar resultados diferentes quando o modelo é implantado em tempo real, consulte [compatibilidade de fórmula do DAX no modo DirectQuery (SQL Server Analysis Services)](http://msdn.microsoft.com/en-us/981b6a68-434d-4db6-964e-d92f8eb3ee3e).|  
|**Limitações de MDX**|Nenhum nome de objeto relativo. Todos os nomes de objeto devem estar totalmente qualificados.<br /><br /> Nenhuma instrução MDX no escopo da sessão (conjuntos nomeados, membros calculados, células calculadas, totais visuais, membros padrão e assim por diante), mas você pode usar construções no escopo da consulta, como a cláusula 'WITH'.<br /><br /> Não há tuplas com membros de níveis diferentes em cláusulas de subseleção MDX.<br /><br /> Não há hierarquias definidas pelo usuário.<br /><br /> Não há nenhuma consulta SQL nativa (normalmente, o Analysis Services dá suporte a um subconjunto T-SQL, mas não para modelos DirectQuery).|  

## <a name="data-sources-supported-for-directquery"></a>Fontes de dados com suporte no DirectQuery
Modelos de tabela DirectQuery no nível de compatibilidade 1200 e superior são compatíveis com as seguintes fontes de dados e provedores:

Fonte de dados   |Versões  |Provedores
---------|---------|---------
Microsoft SQL Server    |  2008 e posterior      |       Provedor OLE DB para SQL Server, Provedor OLE DB para SQL Server Native Client, Provedor de Dados .NET Framework para SQL Client  
Banco de Dados SQL do Microsoft Azure    |   Todos      |  Provedor OLE DB para SQL Server, Provedor OLE DB para SQL Server Native Client, Provedor de Dados .NET Framework para SQL Client            
SQL Data Warehouse do Microsoft Azure     |   Todos     |  Provedor de dados .NET Framework para SQL Client       
Microsoft SQL APS (Analytics Platform System)     |   Todos      |  Provedor OLE DB para SQL Server, Provedor OLE DB para SQL Server Native Client, Provedor de Dados .NET Framework para SQL Client       
Bancos de dados relacionais da Oracle     |  Oracle 9i e posterior       |  Provedor OLE DB Oracle       
Bancos de dados relacionais do Teradata    |  Teradata V2R6 e posterior     | Provedor de .NET Data para Teradata        

## <a name="connecting-to-a-data-source"></a>Conectando-se a uma fonte de dados
Ao criar um modelo do DirectQuery no SSDT, a conexão a uma fonte de dados e a seleção das tabelas e dos campos a serem incluídos no modelo são idênticas ao procedimento com os modelos na memória. 

Se você já tiver ativado o DirectQuery, mas ainda não se conectou a uma fonte de dados, poderá usar o Assistente de Importação de Tabela para se conectar à fonte de dados, selecionar tabelas e campos, especificar uma consulta SQL e assim por diante. Haverá uma diferença quando você terminar: nenhum dado é realmente importado para o cache na memória. 

![Êxito de importação do DirectQuery](../../analysis-services/tabular-models/media/directquery-import-success.png)

Se você já tiver usado o Assistente de Importação de Tabela para importar dados, mas ainda não ativou o modo DirectQuery, quando você fizer isso, o cache na memória será limpo.

  
## <a name="additional-articles-in-this-section"></a>Artigos nesta seção
[Habilitar o modo DirectQuery no SSDT](../../analysis-services/tabular-models/enable-directquery-mode-in-ssdt.md)

[Habilitar o modo DirectQuery no SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[Adicionar dados de exemplo a um modelo DirectQuery no Modo de Design](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)

[Definir partições em modelos DirectQuery](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)
  
[Testar um modelo no modo DirectQuery](../../analysis-services/tabular-models/test-a-model-in-directquery-mode.md)

[Compatibilidade de fórmula do DAX no modo DirectQuery](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md)
  
