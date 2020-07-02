---
title: Especificando predicados em uma etapa de expressão de caminho | Microsoft Docs
description: Saiba como especificar predicados na etapa eixo de uma expressão de caminho XQuery para filtrar uma sequência de nós XML.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- predicates [XQuery]
- qualifiers [XQuery]
- path expressions [XQuery]
ms.assetid: 2660ceca-b8b4-4a1f-98a0-719ad5f89f81
author: rothja
ms.author: jroth
ms.openlocfilehash: a0945ffa8845c901662acb29c3ed04826870d0ae
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722599"
---
# <a name="path-expressions---specifying-predicates"></a>Expressões de Caminho – Especificar Predicados
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Conforme descrito no tópico, as [expressões de caminho no XQuery](../xquery/path-expressions-xquery.md), uma etapa de eixo em uma expressão de caminho inclui os seguintes componentes:  
  
-   [Um eixo](../xquery/path-expressions-specifying-axis.md).  
  
-   Um teste de nó. Para obter mais informações, consulte [especificando o teste de nó em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-node-test.md).  
  
-   Zero ou mais predicados. Isso é opcional.  
  
 O predicado opcional é a terceira parte da etapa de eixo em uma expressão de caminho.  
  
## <a name="predicates"></a>Predicados  
 Um predicado é usado para filtrar uma sequência de nó aplicando-se um teste especificado. A expressão de predicado é inclusa em um colchete e associada ao último nó em uma expressão de caminho.  
  
 Por exemplo, suponha que um valor de parâmetro SQL (x) do tipo de dados **XML** seja declarado, conforme mostrado a seguir:  
  
```  
declare @x xml  
set @x = '  
<People>  
  <Person>  
    <Name>John</Name>  
    <Age>24</Age>  
  </Person>  
  <Person>  
    <Name>Goofy</Name>  
    <Age>54</Age>  
  </Person>  
  <Person>  
    <Name>Daffy</Name>  
    <Age>30</Age>  
  </Person>  
</People>  
'  
```  
  
 Nesse caso, são válidas as seguintes expressões que usam um valor de predicado de [1] em cada um dos três diferentes níveis de nó:  
  
```  
select @x.query('/People/Person/Name[1]')  
select @x.query('/People/Person[1]/Name')  
select @x.query('/People[1]/Person/Name')  
```  
  
 Observe que em cada caso, o predicado associa-se ao nó na expressão de caminho em que ele é aplicado. Por exemplo, a primeira expressão de caminho seleciona o primeiro <`Name` elemento> dentro de cada nó/People/Person e, com a instância XML fornecida, retorna o seguinte:  
  
```  
<Name>John</Name><Name>Goofy</Name><Name>Daffy</Name>  
```  
  
 No entanto, a segunda expressão de caminho seleciona todos os `Name` elementos <> que estão no primeiro nó/People/Person. Portanto, ele retorna o seguinte:  
  
```  
<Name>John</Name>  
```  
  
 Os parênteses também podem ser usados para alterar a ordem de avaliação do predicado. Por exemplo, na expressão a seguir, um conjunto de parênteses é usado para separar o caminho de (/People/Person/Name) do predicado [1]:  
  
```  
select @x.query('(/People/Person/Name)[1]')  
```  
  
 Nesse exemplo, é alterada a ordem em que o predicado é aplicado. Isso acontece porque o caminho incluso é avaliado em primeiro lugar (/People/Person/Name) e, então, o operador do predicado [1] é aplicado ao conjunto que contém todos os nós que corresponderam ao caminho incluso. Sem os parênteses, a ordem de operação seria diferente, de forma que [1] é aplicado como teste de nó `child::Name`, semelhante ao primeiro exemplo de expressão de caminho.  
  
### <a name="quantifiers-and-predicates"></a>Quantificadores e predicados  
 Os quantificadores podem ser usados e adicionados mais de uma vez dentro dos colchetes do próprio predicado. Por exemplo, usando o exemplo anterior, o descrito a seguir é um uso válido de mais de um quantificador dentro de uma subexpressão de predicado complexo.  
  
```  
select @x.query('/People/Person[contains(Name[1], "J") and xs:integer(Age[1]) < 40]/Name/text()')  
```  
  
 O resultado de uma expressão de predicado é convertido em um valor Booliano e é chamado de valor verdadeiro do predicado. Apenas os nós da sequência para a qual o valor verdadeiro do predicado é True são retornados no resultado. Todos os outros nós são descartados.  
  
 Por exemplo, a expressão de caminho a seguir inclui um predicado em sua segunda etapa:  
  
```  
/child::root/child::Location[attribute::LocationID=10]  
```  
  
 A condição especificada por esse predicado é aplicada a todos os <`Location`> nó filho do elemento. O resultado é que só aqueles locais de centro de trabalho cujo valor do atributo LocationID seja 10 serão retornados.  
  
 A expressão de caminho anterior é executada na seguinte instrução SELECT:  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
 /child::AWMI:root/child::AWMI:Location[attribute::LocationID=10]  
')  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
### <a name="computing-predicate-truth-values"></a>Calculando valores verdadeiros do predicado  
 As regras a seguir são aplicadas de forma a determinar o valor verdadeiro do predicado, de acordo com as especificações do XQuery:  
  
1.  Se o valor da expressão do predicado for uma sequência vazia, o valor verdadeiro do predicado será False.  
  
     Por exemplo:  
  
    ```  
    SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     /child::AWMI:root/child::AWMI:Location[attribute::LotSize]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=7  
    ```  
  
     A expressão de caminho nessa consulta retorna somente os `Location` nós de elemento <> que têm um atributo de lotes especificado. Se o predicado retornar uma sequência vazia para um <específico `Location`>, o local do centro de trabalho não será retornado no resultado.  
  
2.  Os valores de predicado só podem ser xs: Integer, xs: Boolean ou Node \* . Para \* o nó, o predicado será avaliado como true se houver qualquer nó e false para uma sequência vazia. Qualquer outro tipo numérico, como dobro e tipo de float, gera um erro de tipo estático. O valor verdadeiro do predicado de uma expressão é True se e somente se o inteiro resultante for igual ao valor da posição de contexto. Além disso, somente valores literais inteiros e a função **Last ()** reduzem a cardinalidade da expressão de etapa filtrada como 1.  
  
     Por exemplo, a consulta a seguir recupera o terceiro nó filho do elemento <`Features`>.  
  
    ```  
    SELECT CatalogDescription.query('  
    declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /child::PD:ProductDescription/child::PD:Features/child::*[3]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=19  
    ```  
  
     Observe o seguinte na consulta anterior:  
  
    -   A terceira etapa na expressão especifica uma expressão de predicado cujo valor é 3. Portanto, o valor verdadeiro do predicado dessa expressão é True só para aqueles nós cuja posição de contexto é 3.  
  
    -   A terceira etapa também especifica um caractere curinga (*) que indica todos os nós no teste de nó. Porém, o predicado filtra os nós e retorna apenas o nó na terceira posição.  
  
    -   A consulta retorna o terceiro nó filho do elemento <`Features`> filhos do elemento <`ProductDescription`> filhos da raiz do documento.  
  
3.  Se o valor da expressão do predicado é um valor de tipo simples de tipo Booliano, o valor verdadeiro do predicado é igual ao valor da expressão do predicado.  
  
     Por exemplo, a consulta a seguir é especificada em uma variável de tipo **XML**que mantém uma instância XML, a instância XML de pesquisa do cliente. A consulta recupera aqueles clientes que têm filhos. Nesta consulta, isso seria \<HasChildren> 1 \</HasChildren> .  
  
    ```  
    declare @x xml  
    set @x='  
    <Survey>  
      <Customer CustomerID="1" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>1</HasChildren>  
      </Customer>  
      <Customer CustomerID="2" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>0</HasChildren>  
      </Customer>  
    </Survey>  
    '  
    declare @y xml  
    set @y = @x.query('  
      for $c in /child::Survey/child::Customer[( child::HasChildren[1] cast as xs:boolean ? )]  
      return   
          <CustomerWithChildren>  
              { $c/attribute::CustomerID }  
          </CustomerWithChildren>  
    ')  
    select @y  
    ```  
  
     Observe o seguinte na consulta anterior:  
  
    -   A expressão no loop **for** tem duas etapas, e a segunda etapa especifica um predicado. O valor desse predicado é um valor de tipo Booliano. Se esse valor for True, o valor verdadeiro do predicado também será True.  
  
    -   A consulta retorna o <`Customer` elemento> filho, cujo valor de predicado é true, do \<Survey> elemento filho da raiz do documento. Este é o resultado:  
  
        ```  
        <CustomerWithChildren CustomerID="1"/>   
        ```  
  
4.  Se o valor da expressão do predicado é uma sequência que contém no mínimo um nó, o valor verdadeiro do predicado é True.  
  
 Por exemplo, a consulta a seguir recupera ProductModelID para modelos de produto cuja descrição do catálogo XML inclui pelo menos um recurso, um elemento filho do `Features` elemento <>, do namespace associado ao prefixo do **WM** .  
  
```  
SELECT ProductModelID  
FROM   Production.ProductModel  
WHERE CatalogDescription.exist('  
             declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
             /child::PD:ProductDescription/child::PD:Features[wm:*]  
             ') = 1  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A cláusula WHERE especifica o [método exist () (tipo de dados XML)](../t-sql/xml/exist-method-xml-data-type.md).  
  
-   A expressão de caminho dentro do método **exist ()** especifica um predicado na segunda etapa. Se a expressão de predicado retornar uma sequência de pelo menos um recurso, o valor verdadeiro dessa expressão de predicado será True. Nesse caso, como o método **exist ()** retorna um true, o ProductModelID é retornado.  
  
## <a name="static-typing-and-predicate-filters"></a>Digitação estática e filtros de predicado  
 Os predicados também podem afetar estaticamente o tipo inferido de uma expressão. Valores literais inteiros e a função **Last ()** reduzem a cardinalidade da expressão de etapa filtrada para no máximo um.  
  
  
