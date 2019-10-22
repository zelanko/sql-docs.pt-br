---
title: Definir a serialização de dados XML | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- entitization rules [XML in SQL Server]
- serialization
- reparsing serialized XML structures
- encoding [XML in SQL Server]
- XML [SQL Server], serialization
- xml data type [SQL Server], serialization
- typed XML
ms.assetid: 42b0b5a4-bdd6-4a60-b451-c87f14758d4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39f3ccc462fb063ecb314b1e9968dcfa8a095cbb
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688893"
---
# <a name="define-the-serialization-of-xml-data"></a>Definir a serialização de dados XML
  Ao converter o tipo de dados XML explicitamente ou implicitamente em uma cadeia de caracteres SQL ou tipo binário, o conteúdo do tipo de dados XML será serializado de acordo com as regras descritas neste tópico.  
  
## <a name="serialization-encoding"></a>Codificação de serialização  
 Se o tipo de destino SQL for VARBINARY, o resultado será serializado em UTF-16 com uma marca de ordem de UTF-16 bytes na frente, mas sem uma declaração XML. Se o tipo de destino for muito pequeno, um erro será gerado.  
  
 Por exemplo:  
  
```sql
select CAST(CAST(N'<Δ/>' as XML) as VARBINARY(MAX))  
```  
  
 Esse é o resultado:  
  
```  
0xFFFE3C0094032F003E00  
```  
  
 Se o tipo de destino SQL for NVARCHAR ou NCHAR, o resultado será serializado em UTF-16 sem a marca de ordem de byte na frente e sem uma declaração XML. Se o tipo de destino for muito pequeno, um erro será gerado.  
  
 Por exemplo:  
  
```sql
select CAST(CAST(N'<Δ/>' as XML) as NVARCHAR(MAX))  
```  
  
 Esse é o resultado:  
  
```  
<Δ/>  
```  
  
 Se o tipo de destino SQL for VARCHAR ou NCHAR, o resultado será serializado na codificação que corresponde à página de código de agrupamento do banco de dados sem uma marca de ordem de byte ou declaração XML. Se o tipo de destino for muito pequeno ou o valor não puder ser mapeado para a página de código de agrupamento de destino, um erro será gerado.  
  
 Por exemplo:  
  
```sql
select CAST(CAST(N'<Δ/>' as XML) as VARCHAR(MAX))  
```  
  
 Isso pode resultar em um erro, se a página de código do agrupamento atual não puder representar o &#x10300;caractere Unicode, ou ele irá representá-lo na codificação específica.  
  
 Ao retornar resultados XML para o lado do cliente, os dados serão enviados na codificação UTF-16. O provedor do lado do cliente irá expor os dados de acordo com suas regras de API.  
  
## <a name="serialization-of-the-xml-structures"></a>Serialização das estruturas XML  
 O conteúdo de um tipo de dados **XML** é serializado da maneira usual. Especificamente, os nós de elementos são mapeados para a marcação de elemento e os nós de texto são mapeados para o conteúdo de texto. No entanto, as circunstâncias sob as quais os caracteres são entidade definida e como os valores atômicos tipados são serializadas são descritas nas seções a seguir.  
  
## <a name="entitization-of-xml-characters-during-serialization"></a>Definição de caracteres XML durante a serialização  
 Cada estrutura XML serializada deve ser capaz de ser reanalisada. Portanto, alguns caracteres precisam ser serializados de uma maneira entidade definida para preservar a capacidade de ida e volta dos caracteres por meio da fase de normalização do analisador XML. No entanto, alguns caracteres precisam ser entidade definida para que o documento esteja bem formado e, portanto, possa ser analisado. A seguir estão as regras de definição que se aplicam durante a serialização:  
  
-   Os caracteres &, \< e > são sempre entidade definida para &amp;, &lt; e &gt;, respectivamente, se ocorrerem dentro de um valor de atributo ou conteúdo de elemento.  
  
-   Como SQL Server usa uma aspa (U + 0022) para valores de atributo delimitador, as aspas nos valores de atributo são entidade definida como &quot;.  
  
-   Um par substituto é entidade definida como uma única referência de caractere numérico, ao fazer a conversão somente no servidor. Por exemplo, o par substituto U + D800 U + DF00 é entidade definida para a referência de caractere numérico & \#x00010300;.  
  
-   Para proteger uma guia (U + 0009) e um avanço de linha (LF, U + 000A) de ser normalizado durante a análise, eles são entidade definida para suas referências de caracteres numéricos & \#x9; e & \#xA; respectivamente, dentro de valores de atributo.  
  
-   Para evitar que um retorno de carro (CR, U + 000D) seja normalizado durante a análise, ele é entidade definida para sua referência de caractere numérico, & \#xD; dentro dos valores de atributo e do conteúdo do elemento.  
  
-   Para proteger nós de texto que contêm apenas espaços em branco, um dos caracteres de espaço em branco, geralmente o último, é entidade definida como sua referência de caractere numérico. Dessa forma, a nova análise preserva o nó de texto de espaço em branco, independentemente da configuração da manipulação de espaço em branco durante a análise.  
  
 Por exemplo:  
  
```sql
declare @u NVARCHAR(50)  
set @u = N'<a a="  
    '+NCHAR(0xD800)+NCHAR(0xDF00)+N'>">   '+NCHAR(0xA)+N'</a>'  
select CAST(CONVERT(XML,@u,1) as NVARCHAR(50))  
```  
  
 Esse é o resultado:  
  
```  
<a a="  
    𐌀>">     
</a>  
```  
  
 Se você não quiser aplicar a última regra de proteção de espaço em branco, poderá usar a opção de conversão explícita 1 ao converter de **XML** em uma cadeia de caracteres ou tipo binário. Por exemplo, para evitar a definição de entidade, você pode fazer o seguinte:  
  
```sql
select CONVERT(NVARCHAR(50), CONVERT(XML, '<a>   </a>', 1), 1)  
```  
  
 Observe que, o [método Query () (tipo de dados XML)](/sql/t-sql/xml/query-method-xml-data-type) resulta em uma instância de tipo de dados XML. Portanto, qualquer resultado do método **Query ()** que é convertido em uma cadeia de caracteres ou tipo binário é entidade definida de acordo com as regras descritas anteriormente. Se você quiser obter os valores de cadeia de caracteres que não são entidade definida, deverá usar o [método Value () (tipo de dados XML)](/sql/t-sql/xml/value-method-xml-data-type) em vez disso. Veja a seguir um exemplo de como usar o método **Query ()** :  
  
```sql
declare @x xml  
set @x = N'<a>This example contains an entitized char: <.</a>'  
select @x.query('/a/text()')  
```  
  
 Esse é o resultado:  
  
```  
This example contains an entitized char: <.  
```  
  
 Veja a seguir um exemplo de como usar o método **Value ()** :  
  
```sql
select @x.value('(/a/text())[1]', 'nvarchar(100)')  
```  
  
 Esse é o resultado:  
  
```  
This example contains an entitized char: <.  
```  
  
## <a name="serializing-a-typed-xml-data-type"></a>Serializando um tipo de dados XML com tipo  
 Uma instância de tipo de dados **XML** tipada contém valores que são digitados de acordo com seus tipos de esquema XML. Esses valores são serializados de acordo com seu tipo de esquema XML no mesmo formato que a conversão XQuery para xs: String produz. Para obter mais informações, consulte [regras de conversão de tipo em XQuery](/sql/xquery/type-casting-rules-in-xquery).  
  
 Por exemplo, o valor xs: Double 1.34 E1 é serializado para 13,4, conforme mostrado no exemplo a seguir:  
  
```sql
declare @x xml  
set @x =''  
select CAST(@x.query('1.34e1') as nvarchar(50))  
```  
  
 Isso retorna o valor da cadeia de caracteres 13.4.  
  
## <a name="see-also"></a>Consulte também  
 [Regras de conversão de tipo em XQuery](/sql/xquery/type-casting-rules-in-xquery)    
 [CONVERSÃO e conversão &#40;de TRANSACT-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)  
  
  
