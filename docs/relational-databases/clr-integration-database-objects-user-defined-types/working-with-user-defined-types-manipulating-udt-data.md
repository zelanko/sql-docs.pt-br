---
title: Manipulando dados UDT | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- data deletions [CLR integration]
- data insertions [CLR integration]
- CONVERT function
- data updates [CLR integration]
- comparing data
- updating data [CLR integration]
- removing data
- IsByteOrdered property
- variables [CLR integration]
- data manipulation [CLR integration]
- user-defined types [CLR integration], data manipulation
- deleting data
- UDTs [CLR integration], data manipulation
- invoking UDT methods
- inserting data
ms.assetid: 51b1a5f2-7591-4e11-bfe2-d88e0836403f
author: rothja
ms.author: jroth
ms.openlocfilehash: d5ab38e745c619d119e8e4ca477e9e78f4ac7783
ms.sourcegitcommit: 0d34b654f0b3031041959e87f5b4d4f0a1af6a29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2019
ms.locfileid: "74901932"
---
# <a name="working-with-user-defined-types---manipulating-udt-data"></a>Trabalhar com tipos definidos pelo usuário –Manipular dados UDT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O [!INCLUDE[tsql](../../includes/tsql-md.md)] não fornece uma sintaxe especializada para instruções INSERT, UPDATE ou DELETE ao modificar dados nas colunas UDTs (tipos definidos pelo usuário). As funções [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST ou CONVERT são usadas para converter tipos de dados nativos no tipo UDT.  
  
## <a name="inserting-data-in-a-udt-column"></a>Inserindo dados em uma coluna UDT  
 As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir inserem três linhas de dados de exemplo na tabela **Points** . O tipo de dados **Point** consiste em valores inteiros X e Y expostos como propriedades de UDT. Você deve usar a função CAST ou CONVERT para converter os valores X e Y delimitados por vírgula para o tipo de **ponto** . As duas primeiras instruções usam a função CONVERT para converter um valor de cadeia de caracteres para o tipo de **ponto** e a terceira instrução usa a função Cast:  
  
```sql  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
## <a name="selecting-data"></a>Selecionando dados  
 A instrução SELECT a seguir seleciona o valor binário do UDT.  
  
```sql  
SELECT ID, PointValue FROM dbo.Points  
```  
  
 Para ver a saída exibida em um formato legível, chame o método **ToString** do **ponto** UDT, que converte o valor em sua representação de cadeia de caracteres.  
  
```sql  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points;  
```  
  
 Isso gera os resultados a seguir.  
  
```  
ID PointValue  
-- ----------  
 1 3,4  
 2 1,5  
 3 1,99  
```  
  
 Você também pode usar as funções [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST e CONVERT para obter os mesmos resultados.  
  
```sql  
SELECT ID, CAST(PointValue AS varchar)   
FROM dbo.Points;  
  
SELECT ID, CONVERT(varchar, PointValue)   
FROM dbo.Points;  
```  
  
 O **ponto** UDT expõe suas coordenadas X e Y como propriedades, que você pode selecionar individualmente. A seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] seleciona as coordenadas X e Y separadamente:  
  
```sql  
SELECT ID, PointValue.X AS xVal, PointValue.Y AS yVal   
FROM dbo.Points;  
```  
  
 As propriedades X e Y retornam um valor inteiro, que é exibido no conjunto de resultados.  
  
```  
ID xVal yVal  
-- ---- ----  
 1    3    4  
 2    1    5  
 3    1   99  
```  
  
## <a name="working-with-variables"></a>Trabalhando com variáveis  
 Você pode trabalhar com variáveis usam a instrução DECLARE para atribuir uma variável a um tipo UDT. As instruções a seguir atribuem um valor usando [!INCLUDE[tsql](../../includes/tsql-md.md)] a instrução SET e exibem os resultados chamando o método **ToString** de UDT na variável:  
  
```sql  
DECLARE @PointValue Point;  
SET @PointValue = (SELECT PointValue FROM dbo.Points  
    WHERE ID = 2);  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 O conjunto de resultados exibe o valor da variável:  
  
```  
PointValue  
----------  
-1,5  
```  
  
 As seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] obtêm o mesmo resultado que usar SELECT em vez de SET para a atribuição de variável:  
  
```sql  
DECLARE @PointValue Point;  
SELECT @PointValue = PointValue FROM dbo.Points  
    WHERE ID = 2;  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 A diferença entre usar SELECT e SET para a atribuição de variável é que SELECT permite atribuir muitas variáveis a uma única instrução SELECT, ao passo que a sintaxe SET exige que cada atribuição de variável tenha sua própria instrução SET.  
  
## <a name="comparing-data"></a>Comparando dados  
 Você pode usar operadores de comparação para comparar valores em seu UDT se tiver definido a propriedade **IsByteOrdered** como **true** ao definir a classe. Para obter mais informações, consulte [criando um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md).  
  
```sql  
SELECT ID, PointValue.ToString() AS Points   
FROM dbo.Points  
WHERE PointValue > CONVERT(Point, '2,2');  
```  
  
 Você pode comparar valores internos do UDT independentemente da configuração **IsByteOrdered** se os próprios valores forem comparáveis. A seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] seleciona linhas onde X é maior que Y:  
  
```sql  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points  
WHERE PointValue.X < PointValue.Y;  
```  
  
 Você também pode usar operadores de comparação com variáveis, como mostrado nesta consulta que procura um PointValue compatível.  
  
```sql  
DECLARE @ComparePoint Point;  
SET @ComparePoint = CONVERT(Point, '3,4');  
SELECT ID, PointValue.ToString() AS MatchingPoint   
FROM dbo.Points  
WHERE PointValue = @ComparePoint;  
```  
  
## <a name="invoking-udt-methods"></a>Invocando métodos UDT   
 Você também pode invocar métodos definidos em seu UDT no [!INCLUDE[tsql](../../includes/tsql-md.md)]. A classe **Point** contém três métodos, **Distance**, **DistanceFrom**e **DistanceFromXY**. Para as listagens de código que definem esses três métodos, consulte [codificação de tipos definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
 A instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir chama o método **PointValue. distance** :  
  
```sql  
SELECT ID, PointValue.X AS [Point.X],   
    PointValue.Y AS [Point.Y],  
    PointValue.Distance() AS DistanceFromZero   
FROM dbo.Points;  
```  
  
 Os resultados são exibidos na coluna **distância** :  
  
```  
ID X  Y  Distance  
-- -- -- ----------------  
 1  3  4                5  
 2  1  5 5.09901951359278  
 3  1 99 99.0050503762308  
```  
  
 O método **DistanceFrom** usa um argumento de tipo de dados **Point** e exibe a distância do ponto especificado para o PointValue:  
  
```sql  
SELECT ID, PointValue.ToString() AS Pnt,  
   PointValue.DistanceFrom(CONVERT(Point, '1,99')) AS DistanceFromPoint  
FROM dbo.Points;  
```  
  
 Os resultados exibem os resultados do método **DistanceFrom** para cada linha na tabela:  
  
```  
ID Pnt DistanceFromPoint  
-- --- -----------------  
 1 3,4  95.0210502993942  
 2 1,5                94  
 3 1,9                90  
```  
  
 O método **DistanceFromXY** usa os pontos individualmente como argumentos:  
  
```sql  
SELECT ID, PointValue.X as X, PointValue.Y as Y,   
PointValue.DistanceFromXY(1, 99) AS DistanceFromXY   
FROM dbo.Points  
```  
  
 O conjunto de resultados é o mesmo que o método **DistanceFrom** .  
  
## <a name="updating-data-in-a-udt-column"></a>Atualizando dados em uma coluna UDT  
 Para atualizar dados em uma coluna UDT, use a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE. Você também pode usar um método do UDT para atualizar o estado do objeto. A seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] atualiza uma única linha na tabela:  
  
```sql  
UPDATE dbo.Points  
SET PointValue = CAST('1,88' AS Point)  
WHERE ID = 3  
```  
  
 Você também pode atualizar elementos UDT separadamente. A seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] atualiza somente a coordenada Y:  
  
```sql  
UPDATE dbo.Points  
SET PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Se o UDT tiver sido definido com a ordenação de **** bytes definida [!INCLUDE[tsql](../../includes/tsql-md.md)] como true, o poderá avaliar a coluna UDT em uma cláusula WHERE.  
  
```sql  
UPDATE dbo.Points  
SET PointValue = '4,5'  
WHERE PointValue = '3,4';  
```  
  
### <a name="updating-limitations"></a>Atualizando limitações  
 Você não pode atualizar várias propriedades de uma ver usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por exemplo, a instrução UPDATE a seguir apresenta uma falha porque você não pode usar o mesmo nome de coluna duas vezes em uma única instrução UDATE.  
  
```sql  
UPDATE dbo.Points  
SET PointValue.X = 5, PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Para atualizar cada ponto individualmente, você precisaria criar um método modificador no assembly UDT Point. Você pode invocar o método modificador para atualizar o objeto em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE, da seguinte maneira:  
  
```sql  
UPDATE dbo.Points  
SET PointValue.SetXY(5, 99)  
WHERE ID = 3  
```  
  
## <a name="deleting-data-in-a-udt-column"></a>Excluindo dados em uma coluna UDT  
 Para excluir dados em um UDT, use a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE. A instrução a seguir exclui todas as linhas da tabela que correspondem aos critérios especificadas na cláusula WHERE. Se você omitir a cláusula WHERE em uma instrução DELETE, todas as linhas da tabela serão excluídas.  
  
```sql  
DELETE FROM dbo.Points  
WHERE PointValue = CAST('1,99' AS Point)  
```  
  
 Use a instrução UPDATE se quiser remover os valores em uma coluna UDT e deixar os valores de outras linhas intactos. Este exemplo define PointValue como nulo.  
  
```sql  
UPDATE dbo.Points  
SET PointValue = null  
WHERE ID = 2  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com tipos de dados definidos pelo usuário no SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
  
  
