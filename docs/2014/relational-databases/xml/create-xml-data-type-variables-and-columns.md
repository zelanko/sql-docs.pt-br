---
title: Criar variáveis e colunas de tipo de dados XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml data type [SQL Server], variables
- xml data type [SQL Server], columns
ms.assetid: 8994ab6e-5519-4ba2-97a1-fac8af6f72db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fe1414131991a35b316a50da730f42e8b02d462
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62637989"
---
# <a name="create-xml-data-type-variables-and-columns"></a>Criar variáveis e colunas de tipo de dados XML
  O tipo de dados `xml` é um tipo de dados interno no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e é um pouco semelhante a outros tipos internos, como `int` e `varchar`. Como com outros tipos internos, você pode usar o `xml` tipo de dados como um tipo de coluna quando você cria uma tabela como um tipo de variável, um tipo de parâmetro, um tipo de retorno de função, ou em [CAST e CONVERT](/sql/t-sql/functions/cast-and-convert-transact-sql).  
  
## <a name="creating-columns-and-variables"></a>Criando colunas e variáveis  
 Para criar uma coluna de tipo `xml` como parte de uma tabela, use uma instrução `CREATE TABLE` , conforme mostrado no exemplo a seguir:  
  
```  
CREATE TABLE T1(Col1 int primary key, Col2 xml)   
```  
  
 É possível usar uma `DECLARE statement` para criar uma variável de tipo `xml` , conforme mostrado no exemplo a seguir.  
  
```  
DECLARE @x xml   
```  
  
 Crie uma variável `xml` com tipo especificando uma coleção de esquema XML, conforme mostrado no exemplo a seguir.  
  
```  
DECLARE @x xml (Sales.StoreSurveySchemaCollection)  
```  
  
 Para passar um parâmetro de tipo `xml` para um procedimento armazenado, use uma instrução `CREATE PROCEDURE` , conforme mostrado no exemplo a seguir:  
  
```  
CREATE PROCEDURE SampleProc(@XmlDoc xml) AS ...   
```  
  
 É possível usar XQuery para consultar instâncias XML armazenadas em colunas, parâmetros ou variáveis. Também é possível usar o XML DML (linguagem de manipulação de dados) para aplicar alterações nas instâncias XML. Como o padrão XQuery não definiu XQuery DML durante o desenvolvimento, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] introduz extensões da [Linguagem de modificação de dados XML](/sql/t-sql/xml/xml-data-modification-language-xml-dml) ao XQuery. Essas extensões permitem executar operações de inserção, atualização e exclusão.  
  
## <a name="assigning-defaults"></a>Atribuindo padrões  
 Em uma tabela, é possível atribuir uma instância XML padrão a uma coluna de tipo `xml`. É possível fornecer o XML padrão de uma de duas maneiras: usando uma constante XML ou usando uma conversão explícita para o tipo `xml`.  
  
 Para fornecer o XML padrão como uma constante XML, use sintaxe conforme mostrado no exemplo a seguir. Observe que a cadeia de caracteres é implicitamente CAST para tipo `xml`.  
  
```  
CREATE TABLE T (XmlColumn xml default N'<element1/><element2/>')  
```  
  
 Para fornecer o XML padrão como um `CAST` explícito para `xml`, use a sintaxe mostrada no exemplo a seguir.  
  
```  
CREATE TABLE T (XmlColumn xml   
                  default CAST(N'<element1/><element2/>' AS xml))  
```  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também oferece suporte a restrições de NULL e NOT NULL em colunas de tipo `xml`. Por exemplo:  
  
```  
CREATE TABLE T (XmlColumn xml NOT NULL)  
```  
  
## <a name="specifying-constraints"></a>Especificando restrições  
 Ao criar colunas de tipo `xml`, é possível definir nível de coluna ou restrições em nível de tabela. Use restrições nas situações seguintes:  
  
-   Suas regras de negócio não podem ser expressas em esquemas XML. Por exemplo, o endereço de entrega de uma floricultura deve estar dentro de 50 milhas do local da empresa. Isto pode ser escrito como uma restrição na coluna XML. A restrição pode envolver métodos de tipo de dados `xml`.  
  
-   A restrição envolve outras colunas XML ou não XML na tabela. Um exemplo é a imposição da ID de um cliente (`/Customer/@CustId`) localizado em uma instância XML para que corresponda ao valor em uma coluna CustomerID relacional.  
  
 Você pode especificar restrições para colunas de tipo de dados `xml` com tipo ou sem-tipo. No entanto não é possível usar os [Métodos de tipo de dados XML](/sql/t-sql/xml/xml-data-type-methods) quando você especifica restrições. Observe também que o tipo de dados `xml` não oferece suporte às seguintes restrições de tabela e coluna:  
  
-   PRIMARY KEY/ FOREIGN KEY  
  
-   UNIQUE  
  
-   COLLATE  
  
     O XML fornece sua própria codificação. Ordenações são aplicadas apenas a tipos de cadeia de caracteres. O tipo de dados `xml` não é um tipo de cadeia de caracteres. No entanto ele tem representação de cadeia de caracteres e permite conversão em tipos de cadeia de caracteres e vice-versa.  
  
-   RULE  
  
 Uma alternativa ao uso de restrições é criar um wrapper, função definida pelo usuário para encapsular o método de tipo de dados `xml` e especificar função definida pelo usuário na restrição de verificação, conforme mostrado no exemplo a seguir.  
  
 No exemplo a seguir, a restrição na `Col2` especifica que cada instância XML armazenada nessa coluna deve ter um elemento `<ProductDescription>` que contém um atributo `ProductID` . Essa restrição é imposta pela função definida pelo usuário:  
  
```  
CREATE FUNCTION my_udf(@var xml) returns bit  
AS BEGIN   
RETURN @var.exist('/ProductDescription/@ProductID')  
END  
GO  
```  
  
 Observe que o método `exist()` do tipo de dados `xml` retornará `1` se o elemento `<ProductDescription>` na instância contiver o atributo `ProductID` . Caso contrário, ele retornará `0`.  
  
 Agora, você pode criar uma tabela com uma restrição em nível de coluna da seguinte maneira:  
  
```  
CREATE TABLE T (  
    Col1 int primary key,   
    Col2 xml check(dbo.my_udf(Col2)=1))  
GO  
```  
  
 A seguinte inserção é feita com êxito:  
  
```  
INSERT INTO T values(1,'<ProductDescription ProductID="1" />')  
```  
  
 Por causa da restrição, a seguinte inserção não tem êxito:  
  
```  
INSERT INTO T values(1,'<Product />')  
```  
  
## <a name="same-or-different-table"></a>Mesma tabela ou tabela diferente  
 Um `xml` coluna de tipo de dados pode ser criada em uma tabela que contém outras colunas relacionais ou em uma tabela separada com uma relação de chave estrangeira com uma tabela principal.  
  
 Criar um `xml` coluna de tipo de dados na mesma tabela quando uma das seguintes condições for verdadeira:  
  
-   O aplicativo executa recuperação de dados na coluna XML e não requer um índice XML na coluna XML.  
  
-   Você deseja criar um índice XML na coluna de tipo de dados `xml` e a chave primária da tabela principal é a mesma que sua chave de clustering. Para obter mais informações, veja [Índices XML &#40;SQL Server&#41;](xml-indexes-sql-server.md).  
  
 Crie uma coluna de tipo de dados `xml`na mesma tabela quando um das seguintes condições for verdadeira:  
  
-   Você deseja criar um índice XML na coluna de tipo de dados `xml`, mas a chave primária da tabela principal é diferente de sua chave de clustering ou a tabela principal não tem uma chave primária ou a tabela principal é um heap (sem chave de clustering). Isto poderá ser verdade se a tabela principal já existir.  
  
-   Você não deseja que as verificações de tabela se tornem mais lentas por causa da presença da coluna XML na tabela. Isso usará espaço se for armazenado dentro da linha ou fora da linha.  
  
  
