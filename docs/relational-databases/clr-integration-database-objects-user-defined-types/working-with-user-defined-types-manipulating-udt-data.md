---
title: Manipulando dados UDT | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: baf3dad1ff4db835e825eacf9a411d56c7d72923
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37354268"
---
# <a name="working-with-user-defined-types---manipulating-udt-data"></a>Trabalhando com tipos definidos pelo usuário – manipulando dados UDT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O [!INCLUDE[tsql](../../includes/tsql-md.md)] não fornece uma sintaxe especializada para instruções INSERT, UPDATE ou DELETE ao modificar dados nas colunas UDTs (tipos definidos pelo usuário). As funções [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST ou CONVERT são usadas para converter tipos de dados nativos no tipo UDT.  
  
## <a name="inserting-data-in-a-udt-column"></a>Inserindo dados em uma coluna UDT  
 O seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções inserirem três linhas de dados de exemplo para o **pontos** tabela. O **ponto** tipo de dados consiste em X e Y inteiro valores que são expostas como propriedades do UDT. Você deve usar a função CAST ou CONVERT para converter o delimitada por vírgulas para valores de X e Y para o **ponto** tipo. As duas primeiras instruções usam a função CONVERT para converter um valor de cadeia de caracteres para o **ponto** tipo e a terceira instrução usa a função CAST:  
  
```  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
## <a name="selecting-data"></a>Selecionando dados  
 A instrução SELECT a seguir seleciona o valor binário do UDT.  
  
```  
SELECT ID, PointValue FROM dbo.Points  
```  
  
 Para ver a saída exibida em um formato legível, chame o **ToString** método o **ponto** UDT, que converte o valor em sua representação de cadeia de caracteres.  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points;  
```  
  
 Isso gera os resultados a seguir.  
  
```  
IDPointValue  
----------  
13,4  
21,5  
31,99  
```  
  
 Você também pode usar as funções [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST e CONVERT para obter os mesmos resultados.  
  
```  
SELECT ID, CAST(PointValue AS varchar)   
FROM dbo.Points;  
  
SELECT ID, CONVERT(varchar, PointValue)   
FROM dbo.Points;  
```  
  
 O **ponto** UDT expõe suas coordenadas X e Y como propriedades, que você pode selecionar individualmente. A seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] seleciona as coordenadas X e Y separadamente:  
  
```  
SELECT ID, PointValue.X AS xVal, PointValue.Y AS yVal   
FROM dbo.Points;  
```  
  
 As propriedades X e Y retornam um valor inteiro, que é exibido no conjunto de resultados.  
  
```  
IDxValyVal  
----------  
134  
215  
3199  
```  
  
## <a name="working-with-variables"></a>Trabalhando com variáveis  
 Você pode trabalhar com variáveis usam a instrução DECLARE para atribuir uma variável a um tipo UDT. As seguintes instruções atribuem um valor usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução SET e exibem os resultados chamando o UDT **ToString** método na variável:  
  
```  
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
  
```  
DECLARE @PointValue Point;  
SELECT @PointValue = PointValue FROM dbo.Points  
    WHERE ID = 2;  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 A diferença entre usar SELECT e SET para a atribuição de variável é que SELECT permite atribuir muitas variáveis a uma única instrução SELECT, ao passo que a sintaxe SET exige que cada atribuição de variável tenha sua própria instrução SET.  
  
## <a name="comparing-data"></a>Comparando dados  
 Você pode usar operadores de comparação para comparar valores em seu UDT se você tiver definido o **IsByteOrdered** propriedade **verdadeiro** ao definir a classe. Para obter mais informações, consulte [criando um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md).  
  
```  
SELECT ID, PointValue.ToString() AS Points   
FROM dbo.Points  
WHERE PointValue > CONVERT(Point, '2,2');  
```  
  
 Você pode comparar valores internos do UDT independentemente do **IsByteOrdered** configuração se os próprios valores forem comparáveis. A seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] seleciona linhas onde X é maior que Y:  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points  
WHERE PointValue.X < PointValue.Y;  
```  
  
 Você também pode usar operadores de comparação com variáveis, como mostrado nesta consulta que procura um PointValue compatível.  
  
```  
DECLARE @ComparePoint Point;  
SET @ComparePoint = CONVERT(Point, '3,4');  
SELECT ID, PointValue.ToString() AS MatchingPoint   
FROM dbo.Points  
WHERE PointValue = @ComparePoint;  
```  
  
## <a name="invoking-udt-methods"></a>Invocando métodos UDT   
 Você também pode invocar métodos definidos em seu UDT no [!INCLUDE[tsql](../../includes/tsql-md.md)]. O **ponto** classe contém três métodos, **distância**, **DistanceFrom**, e **DistanceFromXY**. Para as listagens de código definem esses três métodos, consulte [Codificando tipos](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
 O seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução chamadas a **PointValue.Distance** método:  
  
```  
SELECT ID, PointValue.X AS [Point.X],   
    PointValue.Y AS [Point.Y],  
    PointValue.Distance() AS DistanceFromZero   
FROM dbo.Points;  
```  
  
 Os resultados são exibidos na **distância** coluna:  
  
```  
IDXYDistance  
------------------------  
1345  
2155.09901951359278  
319999.0050503762308  
```  
  
 O **DistanceFrom** método usa um argumento de **aponte** tipo de dados e exibe a distância do ponto especificado até o PointValue:  
  
```  
SELECT ID, PointValue.ToString() AS Pnt,  
   PointValue.DistanceFrom(CONVERT(Point, '1,99')) AS DistanceFromPoint  
FROM dbo.Points;  
```  
  
 Os resultados exibem os resultados do **DistanceFrom** método para cada linha na tabela:  
  
```  
ID PntDistanceFromPoint  
---------------------  
13,495.0210502993942  
21,594  
31,990  
```  
  
 O **DistanceFromXY** método usa os pontos individualmente como argumentos:  
  
```  
SELECT ID, PointValue.X as X, PointValue.Y as Y,   
PointValue.DistanceFromXY(1, 99) AS DistanceFromXY   
FROM dbo.Points  
```  
  
 O conjunto de resultados é igual a **DistanceFrom** método.  
  
## <a name="updating-data-in-a-udt-column"></a>Atualizando dados em uma coluna UDT  
 Para atualizar dados em uma coluna UDT, use a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE. Você também pode usar um método do UDT para atualizar o estado do objeto. A seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] atualiza uma única linha na tabela:  
  
```  
UPDATE dbo.Points  
SET PointValue = CAST('1,88' AS Point)  
WHERE ID = 3  
```  
  
 Você também pode atualizar elementos UDT separadamente. A seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] atualiza somente a coordenada Y:  
  
```  
UPDATE dbo.Points  
SET PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Se o UDT foi definido com a ordenação de bytes definida para **verdadeira**, [!INCLUDE[tsql](../../includes/tsql-md.md)] pode avaliar a coluna UDT em uma cláusula WHERE.  
  
```  
UPDATE dbo.Points  
SET PointValue = '4,5'  
WHERE PointValue = '3,4';  
```  
  
### <a name="updating-limitations"></a>Atualizando limitações  
 Você não pode atualizar várias propriedades de uma ver usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por exemplo, a instrução UPDATE a seguir apresenta uma falha porque você não pode usar o mesmo nome de coluna duas vezes em uma única instrução UDATE.  
  
```  
UPDATE dbo.Points  
SET PointValue.X = 5, PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Para atualizar cada ponto individualmente, você precisaria criar um método modificador no assembly UDT Point. Você pode invocar o método modificador para atualizar o objeto em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE, da seguinte maneira:  
  
```  
UPDATE dbo.Points  
SET PointValue.SetXY(5, 99)  
WHERE ID = 3  
```  
  
## <a name="deleting-data-in-a-udt-column"></a>Excluindo dados em uma coluna UDT  
 Para excluir dados em um UDT, use a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE. A instrução a seguir exclui todas as linhas da tabela que correspondem aos critérios especificadas na cláusula WHERE. Se você omitir a cláusula WHERE em uma instrução DELETE, todas as linhas da tabela serão excluídas.  
  
```  
DELETE FROM dbo.Points  
WHERE PointValue = CAST('1,99' AS Point)  
```  
  
 Use a instrução UPDATE se quiser remover os valores em uma coluna UDT e deixar os valores de outras linhas intactos. Este exemplo define PointValue como nulo.  
  
```  
UPDATE dbo.Points  
SET PointValue = null  
WHERE ID = 2  
```  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com tipos de dados definidos pelo usuário no SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
  
  
