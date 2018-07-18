---
title: SELECT FROM &lt;estrutura&gt;. CASOS | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f473cb42230aec0b5e40fb59fe10b2f34013ba2f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37985258"
---
# <a name="select-from-ltstructuregtcases"></a>SELECT FROM &lt;estrutura&gt;. CASOS
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna os casos usados para criar a estrutura de mineração.  
  
 Se detalhamento não estiver habilitado na estrutura, a instrução falhará. Além disso, a instrução falhará se o usuário não tiver permissões de detalhamento na estrutura de mineração.  
  
 No [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], detalhamento em novas estruturas de mineração está habilitado por padrão. Para verificar se o detalhamento está habilitado para uma determinada estrutura, verifique se o valor da **CacheMode** estiver definida como **KeepTrainingCases**.  
  
 Se o valor de **CacheMode** é alterado para **ClearAfterProcessing**, casos de estrutura serão apagados do cache e você não pode usar o detalhamento.  
  
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
  
 *estrutura*  
 O nome da estrutura.  
  
 *expressão de condição*  
 Uma condição para restringir os valores retornados da lista de colunas.  
  
 *Expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Remarks  
 Se detalhamento for habilitada no modelo e na estrutura, qualquer membro de uma função com permissões de detalhamento na estrutura de mineração e no modelo poderá retornar colunas da estrutura que não foram incluídas no modelo, usando a seguinte sintaxe:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Portanto, para proteger dados confidenciais ou informações pessoais, você deve construir sua exibição da fonte de dados para mascarar informações pessoais e conceder **AllowDrillthrough** permissão em uma estrutura de mineração ou modelo de mineração somente quando necessário.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir baseiam-se na estrutura de mineração, destinada, que se baseia o [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] banco de dados e modelos de mineração associados. Para obter mais informações, consulte [Tutorial básico de mineração de dados](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [SELECIONE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
