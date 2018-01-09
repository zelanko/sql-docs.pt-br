---
title: SELECT FROM &lt;estrutura&gt;. CASOS | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- CASES
- FROM
dev_langs: DMX
helpviewer_keywords: SELECT FROM <structure> statements
ms.assetid: 36f50213-14dc-42da-b899-20240b781e1a
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 877f35988bceb86425b4517eb331ce526b9168f8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="select-from-ltstructuregtcases"></a>SELECT FROM &lt;estrutura&gt;. CASOS
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna os casos usados para criar a estrutura de mineração.  
  
 Se detalhamento não estiver habilitado na estrutura, a instrução falhará. Além disso, a instrução falhará se o usuário não tiver permissões de detalhamento na estrutura de mineração.  
  
 Em [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], detalhamento em novas estruturas de mineração é habilitado por padrão. Para verificar se o detalhamento está habilitado para uma estrutura específica, verifique se o valor da **CacheMode** está definida como **KeepTrainingCases**.  
  
 Se o valor de **CacheMode** é alterado para **ClearAfterProcessing**, os casos de estrutura serão apagados do cache e não é possível usar o detalhamento.  
  
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
  
 *expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Remarks  
 Se detalhamento for habilitada no modelo e na estrutura, qualquer membro de uma função com permissões de detalhamento na estrutura de mineração e no modelo poderá retornar colunas da estrutura que não foram incluídas no modelo, usando a seguinte sintaxe:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Portanto, para proteger dados confidenciais ou informações pessoais, você deve construir sua exibição da fonte de dados para mascarar informações pessoais e atribuir **AllowDrillthrough** permissão em uma estrutura de mineração ou modelo de mineração somente quando necessário.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir baseiam-se na estrutura de mineração, correspondência destinada, que se baseia o [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] banco de dados e modelos de mineração associados. Para obter mais informações, consulte [Tutorial básico de mineração de dados](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
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
 [SELECIONAR &#40; DMX &#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
