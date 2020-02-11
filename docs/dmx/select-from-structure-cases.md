---
title: Selecione da &lt;estrutura&gt;. CASOS | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 041d6ade2363b4a33528bd44438a2fcb440d61ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928291"
---
# <a name="select-from-ltstructuregtcases"></a>Selecione da &lt;estrutura&gt;. BOLSAS
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna os casos usados para criar a estrutura de mineração.  
  
 Se detalhamento não estiver habilitado na estrutura, a instrução falhará. Além disso, a instrução falhará se o usuário não tiver permissões de detalhamento na estrutura de mineração.  
  
 No [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], o detalhamento em novas estruturas de mineração é habilitado por padrão. Para verificar se o detalhamento está habilitado para uma determinada estrutura, verifique se o valor da propriedade **CacheMode** está definido como **KeepTrainingCases**.  
  
 Se o valor de **CacheMode** for alterado para **ClearAfterProcessing**, os casos de estrutura serão apagados do cache e você não poderá usar o detalhamento.  
  
> [!NOTE]  
>  Não é possível habilitar ou desabilitar o detalhamento na estrutura de mineração usando DMX (Data Mining Extensions).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT [TOP n] <expression list> FROM <structure>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Um inteiro que especifica quantas linhas serão retornadas.  
  
 *lista de expressões*  
 Uma lista de expressões separadas por vírgulas.  
  
 Uma expressão pode incluir identificadores de coluna, funções definidas pelo usuário e funções VBA.  
  
 *estruturá*  
 O nome da estrutura.  
  
 *expressão de condição*  
 Uma condição para restringir os valores retornados da lista de colunas.  
  
 *expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Se detalhamento for habilitada no modelo e na estrutura, qualquer membro de uma função com permissões de detalhamento na estrutura de mineração e no modelo poderá retornar colunas da estrutura que não foram incluídas no modelo, usando a seguinte sintaxe:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Portanto, para proteger dados confidenciais ou informações pessoais, você deve construir sua exibição da fonte de dados para mascarar informações pessoais e conceder a permissão **AllowDrillThrough** em uma estrutura de mineração ou modelo de mineração somente quando necessário.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir são baseados na estrutura de mineração, mala direta, que se baseia no banco [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] de dados e nos modelos de mineração associados. Para obter mais informações, consulte o [tutorial básico de mineração de dados](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
### <a name="example-1-drill-through-to-structure-cases"></a>Exemplo 1: detalhamento para casos da estrutura  
 O seguinte exemplo retorna uma lista dos 500 clientes mais antigos na estrutura de mineração, Correspondência destinada. A consulta retorna todas as colunas no modelo de mineração, mas restringe as linhas para as que compraram uma bicicleta e as classifica por idade. Também é possível editar a lista de expressões para retornar apenas as colunas necesárias.  
  
```  
SELECT TOP 500 *  
FROM [Targeted Mailing].Cases  
WHERE [Bike Buyer] = 1  
ORDER BY Age DESC;  
```  
  
### <a name="example-2-drillthrough-to-test-or-training-cases-only"></a>Exemplo 2: detalhamento apenas para casos de teste ou de treinamento  
 O seguinte exemplo retorna uma lista dos casos da estrutura da Correspondência destinada reservados para teste. Se a estrutura de mineração não contiver um conjunto de testes de validação, por padrão todos os casos serão tratados como casos de treinamento e essa consulta retornará 0 casos.  
  
```  
SELECT [Customer Key], Gender, Age  
FROM [Targeted Mailing].Cases  
WHERE IsTestCase();  
```  
  
 Para retornar os casos de treinamento, substitua a função `IsTrainingCase()`.  
  
## <a name="see-also"></a>Consulte Também  
 [SELECIONAR&#41;&#40;DMX](../dmx/select-dmx.md)   
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
