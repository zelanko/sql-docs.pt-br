---
title: SELECT FROM &lt;modelo&gt;. CASOS (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f65aa4dc64e795235286eccd9f3283216ba6f4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62658763"
---
# <a name="select-from-ltmodelgtcases-dmx"></a>SELECT FROM &lt;model&gt;.CASES (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Suporta o detalhamento e retorna os casos usados para treinar o modelo. Também é possível retornar colunas de estrutura que não foram incluídas no modelo, se o detalhamento tiver sido habilitado na estrutura de mineração e no modelo de mineração e se você tiver as permissões apropriadas.  
  
 Se o detalhamento não estiver habilitado no modelo de mineração, essa instrução falhará.  
  
> [!NOTE]  
>  No DMX (Data Mining Extensions) é possível apenas habilitar o detalhamento ao criar o modelo. É possível adicionar o detalhamento a um modelo existente usando o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], mas o modelo deve ser reprocessado antes de você poder exibir ou consultar os casos.  
  
 Para obter mais informações sobre como habilitar o detalhamento, consulte [criar um modelo de MINERAÇÃO &#40;DMX&#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md), e [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Um inteiro que especifica quantas linhas serão retornadas.  
  
 *lista de expressões*  
 Uma lista de expressões separadas por vírgulas. Uma expressão pode incluir identificadores de coluna, funções definidas pelo usuário, UDFs e funções VBA, além de outras.  
  
 Para incluir uma coluna de estrutura que não foi incluída no modelo de mineração, use a função `StructureColumn('<structure column name>')`.  
  
 *modelo*  
 Identificador de modelo.  
  
 *expressão de condição*  
 Uma condição para restringir os valores retornados da lista de colunas.  
  
 *Expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Se o detalhamento for habilitado no modelo e na estrutura de mineração, os usuários que foram membros de uma função com permissão de detalhamento no modelo e na estrutura poderão acessar as colunas da estrutura de mineração que não foram incluídas no modelo e mineração. Portanto, para proteger dados confidenciais ou informações pessoais, você deve construir sua exibição da fonte de dados para mascarar informações pessoais e conceder **AllowDrillthrough** permissão em uma estrutura de mineração somente quando for necessário.  
  
 O [Lag &#40;DMX&#41; ](../dmx/lag-dmx.md) função pode ser usada com modelos de série temporal para retornar ou filtrar um intervalo de tempo entre cada caso e a hora inicial.  
  
 Usando o [IsInNode &#40;DMX&#41; ](../dmx/isinnode-dmx.md) funcionar a **onde** cláusula retorna somente os casos que estão associados com o nó que é especificado pela coluna NODE_UNIQUE_NAME do conjunto de linhas de esquema.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir baseiam-se na estrutura de mineração destinada, que se baseia o [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]banco de dados e modelos de mineração associados. Para obter mais informações, consulte [Tutorial básico de mineração de dados](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>Exemplo 1: Detalhamento para casos de modelo e colunas de estrutura  
 O seguinte exemplo retorna as colunas para todos os casos usados para testar o modelo Correspondência destinada. Se a estrutura de mineração na qual o modelo foi construído não tiver um conjunto de dados de testes de validação, essa consulta retornará 0 casos. É possível usar a lista de expressões para retornar apenas as colunas necessárias.  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>Exemplo 2: Detalhamento para casos de treinamento em um nó específico  
 O exemplo seguinte retorna apenas os casos usados para treinar o Cluster 2. O nó para o Cluster 2 tem o valor '002' para a coluna de NODE_UNIQUE_NAME. O exemplo também retorna uma coluna de estrutura, [Customer Key], que não faz parte do modelo de mineração e fornece o alias `CustomerID` para a coluna. Observe que o nome da coluna da estrutura é passado como um valor de cadeia de caracteres e, portanto, deve estar entre aspas, não colchetes.  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 Para retornar uma coluna de estrutura, as permissões de detalhamento devem estar habilitadas no modelo de mineração e na estrutura de mineração.  
  
> [!NOTE]  
>  Nem todos os modelos de mineração suportam o detalhamento. Para obter informações sobre os modelos que dão suporte ao detalhamento, consulte [consultas de detalhamento &#40;mineração de dados&#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
