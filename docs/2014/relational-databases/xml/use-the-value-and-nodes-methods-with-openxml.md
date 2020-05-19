---
title: Usar os métodos value() e nodes() com OPENXML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- OpenXML method [XML in SQL Server]
- value method [XML in SQL Server]
- nodes method [XML in SQL Server]
ms.assetid: c73dbe55-d685-42eb-b0ee-9f3c5b9d97f3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 527e646f956e60b2c8495a738a85595baac383f2
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702327"
---
# <a name="use-the-value-and-nodes-methods-with-openxml"></a>Usar os métodos value() e nodes() com OPENXML
  Você pode usar vários métodos **Value ()** no `xml` tipo de dados em uma cláusula **Select** para gerar um conjunto de linhas de valores extraídos. O método **nodes()** produz uma referência interna para cada nó selecionado que pode ser usado para consulta adicional. A combinação dos métodos **nodes()** e **value()** pode ser mais eficiente para gerar o conjunto de linhas quando ele tem várias colunas e, talvez, quando as expressões de caminho usadas em sua geração são complexas.  
  
 O método **Nodes ()** produz instâncias de um `xml` tipo de dados especial, cada um com seu contexto definido como um nó selecionado diferente. Esse tipo de instância XML dá suporte aos métodos **query()** , **value()** , **nodes()** e **exist()** e pode ser usado em agregações **count(\*)** . Todos os outros usos provocam um erro.  
  
## <a name="example-using-nodes"></a>Exemplo: Usando nodes()  
 Assuma que você deseja extrair os nomes e sobrenomes de autores e o nome não é "David". Além disso, você deseja extrair essas informações como um conjunto de linhas que contém duas colunas, FirstName e LastName. Usando os métodos **nodes()** e **value()** , isso pode ser feito da seguinte forma:  
  
```  
SELECT nref.value('(first-name/text())[1]', 'nvarchar(50)') FirstName,  
       nref.value('(last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T CROSS APPLY xCol.nodes('//author') AS R(nref)  
WHERE  nref.exist('first-name[. != "David"]') = 1  
```  
  
 Nesse exemplo, `nodes('//author')` produz um conjunto de linhas de referências a elementos `<author>` para cada instância XML. Os nomes e sobrenomes de autores são obtidos avaliando métodos **value()** em relação a essas referências.  
  
 O SQL Server 2000 fornece a capacidade de gerar um conjunto de linhas de uma instância XML usando **OpenXml()** . É possível especificar o esquema relacional do conjunto de linhas e como valores dentro da instância XML mapeiam para colunas no conjunto de linhas.  
  
## <a name="example-using-openxml-on-the-xml-data-type"></a>Exemplo: Usando OpenXml() no tipo de dados xml  
 A consulta do exemplo anterior pode ser reescrita usando **OpenXml()** conforme mostrado a seguir. Isso é feito criando um cursor que lê cada instância XML em uma variável XML e, em seguida, aplica OpenXML a ela:  
  
```  
DECLARE name_cursor CURSOR  
FOR  
   SELECT xCol   
   FROM   T  
OPEN name_cursor  
DECLARE @xmlVal XML  
DECLARE @idoc int  
FETCH NEXT FROM name_cursor INTO @xmlVal  
  
WHILE (@@FETCH_STATUS = 0)  
BEGIN  
   EXEC sp_xml_preparedocument @idoc OUTPUT, @xmlVal  
   SELECT   *  
   FROM   OPENXML (@idoc, '//author')  
          WITH (FirstName  varchar(50) 'first-name',  
                LastName   varchar(50) 'last-name') R  
   WHERE  R.FirstName != 'David'  
  
   EXEC sp_xml_removedocument @idoc  
   FETCH NEXT FROM name_cursor INTO @xmlVal  
END  
CLOSE name_cursor  
DEALLOCATE name_cursor   
```  
  
 **OpenXml()** cria uma representação na memória e usa tabelas de trabalho em vez do processador de consultas. Ele conta com o processador do XPath versão 1.0 do MSXML versão 3.0 em vez do mecanismo de XQuery. As tabelas de trabalho não são compartilhadas entre várias chamadas para **OpenXml()** , mesmo na mesma instância XML. Isto limita sua escalabilidade. **OpenXml()** permite acessar um formato de tabela de borda para os dados XML quando a cláusula WITH não está especificada. Além disso, ele permite usar o valor XML restante em uma coluna de "estouro" separada.  
  
 A combinação das funções **nodes()** e **value()** usa índices XML de maneira efetiva. Como resultado, essa combinação pode exibir mais escalabilidade que o **OpenXml**.  
  
## <a name="see-also"></a>Consulte Também  
 [OPENXML &#40;SQL Server&#41;](openxml-sql-server.md)  
  
  
