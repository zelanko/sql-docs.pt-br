---
title: StructureColumn (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- StructureColumn
dev_langs:
- DMX
helpviewer_keywords:
- StructureColumn function
ms.assetid: 57557536-4bfa-4fa7-bf7a-fb8722ca200d
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3e7f727e1007c6502e6612ccef563f670837cf5c
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="structurecolumn-dmx"></a>StructureColumn (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o valor da coluna de estrutura que corresponde ao caso especificado ou o valor de tabela para uma tabela aninhada no caso especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StructureColumn('structure column name')  
```  
  
## <a name="arguments"></a>Argumentos  
 nome da coluna da estrutura.  
 O nome de uma coluna da estrutura de mineração de tabela aninhada ou caso.  
  
## <a name="result-type"></a>Tipo de Resultado  
 O tipo retornado depende do tipo da coluna que é referenciado no \<nome de coluna da estrutura > parâmetro. Por exemplo, se a coluna da estrutura de mineração mencionada contiver um valor escalar, a função retornará um valor escalar.  
  
 Se a coluna da estrutura de mineração mencionada for uma tabela aninhada, a função retornará um valor de tabela. O valor de tabela retornado pode ser usado na cláusula FROM de uma instrução sub-SELECT.  
  
## <a name="remarks"></a>Comentários  
 Esta função é polimórfica e pode ser usada em qualquer lugar de uma instrução que permite expressões, incluindo uma lista de expressões SELECT, uma expressão de condição WHERE e uma expressão ORDER BY.  
  
 O nome da coluna na estrutura de mineração é um valor de cadeia de caracteres e como tal, devem ser colocado entre aspas simples: por exemplo, `StructureColumn('` **coluna 1**`')`. Se houver várias colunas com o mesmo nome, o nome será resolvido no contexto da instrução SELECT de circunscrição.  
  
 Os resultados retornados de uma consulta usando o **StructureColumn** função são afetados pela presença de qualquer filtro no modelo. Quer dizer, o filtro do modelo controla os casos que são incluídos no modelo de mineração. Desse modo, uma consulta na coluna de estrutura pode retornar somente os casos que foram usados no modelo de mineração. Consulte a seção Exemplos deste tópico para observar o exemplo de um código que mostra o efeito dos filtros de modelo de mineração nas tabelas de caso e em uma tabela aninhada.  
  
 Para obter mais informações sobre como usar essa função em uma instrução SELECT DMX, consulte [SELECT FROM &#60; modelo de &#62;. CASOS &#40; DMX &#41; ](../dmx/select-from-model-cases-dmx.md) ou [SELECT FROM &#60; estrutura &#62;. CASOS](../dmx/select-from-structure-cases.md).  
  
## <a name="error-messages"></a>Mensagens de erro  
 O erro de segurança a seguir ocorrerá se o usuário não tiver permissão de detalhamento na estrutura de mineração pai:  
  
 O usuário ‘%{user/}’ não tem permissão para detalhar na estrutura de mineração pai do modelo de mineração ‘%{model/}’.  
  
 A mensagem de erro a seguir será exibida se um nome de coluna de estrutura inválido for especificado:  
  
 A coluna de estrutura de mineração ‘%{nome da coluna de estrutura/}’ não foi encontrada na estrutura de mineração pai ‘%{structure/}’ no contexto atual (linha %{line/}, coluna %{column/}).  
  
## <a name="examples"></a>Exemplos  
 Usaremos a seguinte estrutura de mineração para obter estes exemplos. Observe que a estrutura de mineração contém duas colunas de tabela aninhada, `Products` e `Hobbies`. A tabela aninhada na coluna `Hobbies` tem uma única coluna que é usada como a chave para a tabela aninhada. A tabela aninhada na coluna `Products` é uma tabela aninhada complexa que tem uma coluna principal e outras colunas usadas para entrada. Os exemplos a seguir ilustram como uma estrutura de mineração de dados pode ser designada para incluir muitas colunas diferentes, mesmo que um modelo talvez não use todas as colunas. Algumas destas colunas podem não ser úteis no nível do modelo para generalizar padrões, mas podem ser muito úteis para detalhamento.  
  
```  
CREATE MINING STRUCTURE [MyStructure]   
(  
CustomerName TEXT KEY,  
Occupation TEXT DISCRETE,  
Age LONG CONTINUOUS,  
MaritalStatus TEXT DISCRETE,  
Income LONG CONTINUOUS,  
Products  TABLE  
 (  
    ProductNameTEXT KEY,  
    Quantity LONG CONTINUOUS,  
    OnSale BOOLEAN  DISCRETE  
)  
 Hobbies  TABLE  
 (  
    Hobby KEY  
 ))  
```  
  
 Em seguida, crie um modelo de mineração baseado na estrutura que você acabou de criar, usando o código de exemplo a seguir:  
  
```  
ALTER MINING STRUCTURE [MyStructure] ADD MINING MODEL [MyModel] (  
CustomerName,  
Age,  
MaritalStatus,  
Income PREDICT,  
Products   
(  
ProductName  
) WITH FILTER(NOT OnSale)  
) USING Microsoft_Decision_Trees   
WITH FILTER(EXISTS (Products))  
```  
  
### <a name="sample-query-1-returning-a-column-from-the-mining-structure"></a>Consulta de exemplo 1: Retornando uma coluna da estrutura de mineração  
 A consulta de exemplo a seguir retorna as colunas `CustomerName` e `Age`, que fazem parte do modelo de mineração. No entanto, a consulta também retorna a coluna `Age`, que faz parte da estrutura, mas não do modelo de mineração.  
  
```  
SELECT CustomerName, Age, StructureColumn(‘Occupation’) FROM MyModel.CASES   
WHERE Age > 30  
```  
  
 Observe que a filtragem de linhas para restringir os casos a clientes com mais de 30 anos ocorre no nível do modelo. Portanto, esta expressão não retornaria casos que estão incluídos nos dados da estrutura, mas não são usados pelo modelo. Como a condição de filtro usada para criar o modelo (`EXISTS (Products)`) restringe os casos somente aos clientes que adquiriram produtos, podem existir casos na estrutura que não são retornados por esta consulta.  
  
### <a name="sample-query-2-applying-a-filter-to-the-structure-column"></a>Consulta de exemplo 2: Aplicando um filtro à coluna da estrutura  
 A consulta de exemplo a seguir retorna não só as colunas de modelo `CustomerName` e `Age`, e a tabela aninhada `Products`, mas também retorna o valor da coluna `Quantity` na tabela aninhada, que não faz parte do modelo.  
  
```  
SELECT CustomerName, Age,  
(SELECT ProductName, StructureColumn(‘Quantity’) FROM Products) FROM MA.CASES   
WHERE StructureColumn(‘Occupation’) = ‘Architect’  
```  
  
 Observe que, neste exemplo, um filtro é aplicado à coluna de estrutura para restringir os casos para clientes cuja ocupação é 'Arquiteto' (`WHERE StructureColumn(‘Occupation’) = ‘Architect’`). Como a condição de filtro do modelo sempre é aplicada aos casos quando o modelo é criado, somente os casos com pelo menos uma linha qualificada na tabela `Products` são incluídos nos casos do modelo. Desse modo, o filtro no tabela aninhada `Products` e o filtro no caso `(‘Occupation’)` são aplicados.  
  
### <a name="sample-query-3-selecting-columns-from-a-nested-table"></a>Consulta de exemplo 3: Selecionando colunas de uma tabela aninhada  
 A consulta de exemplo a seguir retorna os nomes dos clientes que foram usados como casos de treinamento do modelo. Para cada cliente, a consulta também retorna uma tabela aninhada que contém os detalhes de compra. Embora o modelo inclui a `ProductName` coluna, o modelo não usa o valor de `ProductName` coluna. O modelo só verifica se o produto foi adquirido em regular (`NOT``OnSale`) preço. Esta consulta não só retorna o nome do produto, mas também retorna a quantidade adquirida, que não é incluída no modelo.  
  
```  
SELECT CustomerName,    
(SELECT ProductName, StructureColumn('Quantity')FROM Products)   
FROM MyModel.CASES  
```  
  
 Não é possível retornar a coluna `ProductName` ou a coluna `Quantity` a menos que o detalhamento seja habilitado no modelo de mineração.  
  
### <a name="sample-query-4-filtering-on-and-returning-nested-table-columns"></a>Consulta de exemplo 4: Filtrando e retornando colunas de tabela aninhada  
 A consulta de exemplo a seguir retorna as colunas de tabela aninhada e de caso que são incluídas na estrutura de mineração, mas não no modelo. O modelo já é filtrado na presença de produtos `OnSale`, mas esta consulta adiciona um filtro à coluna da estrutura de mineração, `Quantity`:  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation'),   
(SELECT ProductName, StructureColumn('Quantity') FROM Products)   
FROM MyModel.CASES   
WHERE EXISTS (SELECT * FROM Products WHERE StructureColumn('Quantity')>1)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

