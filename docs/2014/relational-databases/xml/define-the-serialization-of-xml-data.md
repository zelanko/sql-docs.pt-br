---
title: Definir a serialização de dados XML| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
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
ms.openlocfilehash: 759c0200c644913e21262c914957cfa1dcbada5c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62637574"
---
# <a name="define-the-serialization-of-xml-data"></a>Definir a serialização de dados XML
  Ao converter tipos de dados xml explícita ou implicitamente em uma cadeia de caracteres SQL ou tipo binário, o conteúdo do tipo de dados xml será serializado de acordo com as regras descritas neste tópico.  
  
## <a name="serialization-encoding"></a>Codificação de serialização  
 Se o tipo de destino SQL for VARBINARY, o resultado será serializado em UTF-16 com uma marca de ordem de 16 bytes UTF na frente, mas sem uma declaração XML. Se o tipo de destino for muito pequeno, será retornado um erro.  
  
 Por exemplo:   
  
```  
select CAST(CAST(N'<??/>' as XML) as VARBINARY(MAX))  
```  
  
 Esse é o resultado:  
  
```  
0xFFFE3C0094032F003E00  
```  
  
 Se o tipo de destino SQL for NVARCHAR ou NCHAR, o resultado será serializado em UTF-16 sem a marca de ordem de bytes na frente e sem uma declaração XML. Se o tipo de destino for muito pequeno, será retornado um erro.  
  
 Por exemplo:   
  
```  
select CAST(CAST(N'<??/>' as XML) as NVARCHAR(MAX))  
```  
  
 Esse é o resultado:  
  
```  
<??/>  
```  
  
 Se o tipo de destino SQL for VARCHAR ou NCHAR, o resultado será serializado na codificação correspondente à página de código de ordenação do banco de dados sem uma marca de ordem de bytes ou declaração XML. Se o tipo de destino for muito pequeno ou se o valor não puder ser mapeado para a página de código de ordenação de destino, será retornado um erro.  
  
 Por exemplo:  
  
```  
select CAST(CAST(N'<??/>' as XML) as VARCHAR(MAX))  
```  
  
 Isso pode resultar em um erro, se a página de código de agrupamento atual não pode representar o caractere Unicode??, ou ela o representará na codificação específica.  
  
 Ao retornar resultados XML para o lado do cliente, os dados serão enviados em codificação UTF-16. O provedor do lado do cliente exporá os dados de acordo com as regras de sua API.  
  
## <a name="serialization-of-the-xml-structures"></a>Serialização das estruturas XML  
 O conteúdo de um tipo de dados **xml** é serializado da maneira normal. Especificamente, nós de elemento são mapeados para marcação de elemento e nós de texto são mapeados para conteúdo de texto. No entanto, as circunstâncias nas quais a entidade dos caracteres é definida e a maneira como valores atômicos digitados são serializados são descritas nas seções a seguir.  
  
## <a name="entitization-of-xml-characters-during-serialization"></a>Definição da entidade de caracteres XML durante a serialização  
 Cada estrutura XML serializada deve poder ser reanalisada. Portanto alguns caracteres precisam ser serializados de uma maneira de definição de entidade para preservar a capacidade de viagem de ida e volta dos caracteres durante a fase de normalização do analisador XML. No entanto a entidade de alguns caracteres precisa ser definida para que o documento seja bem formado e portanto possa ser analisado. As regras de definição de entidade aplicáveis durante a serialização são as seguintes:  
  
-   Os caracteres &, \< e > são sempre definidos como &amp;, &lt; e &gt; respectivamente, se ocorrem dentro de um valor de atributo ou conteúdo de elemento.  
  
-   Como o SQL Server usa aspas (U+0022) para incluir valores de atributos, a entidade de aspas em valores de atributos é definida como &quot;.  
  
-   A entidade de um par substituto é definida como uma referência de caractere numérico único na conversão no servidor apenas. Por exemplo, a entidade do par substituto U+D800 U+DF00 é definida como a referência de caractere numérico &\#x00010300;.  
  
-   Para proteger uma TABULAÇÃO (U+0009) e um avanço de linha (LF, U+000A) contra normalização durante a análise, suas entidades são definidas como suas referências de caractere numérico &\#x9; e &\#xA; respectivamente, dentro de valores de atributos.  
  
-   Para evitar que um retorno de carro (CR, U+000D) seja normalizado durante a análise, a entidade é definida como sua referência de caractere numérico, &\#xD; dentro dos valores de atributos e do conteúdo de elemento.  
  
-   Para proteger nós de texto que contêm apenas espaço em branco, a entidade de um dos caracteres de espaço em branco, geralmente o último, é definida como sua referência de caractere numérico. Dessa maneira, a reanálise preserva o nó de texto do caractere em branco, independentemente da configuração do tratamento do espaço em branco durante a análise.  
  
 Por exemplo:  
  
```  
declare @u NVARCHAR(50)  
set @u = N'<a a="  
    '+NCHAR(0xD800)+NCHAR(0xDF00)+N'>">   '+NCHAR(0xA)+N'</a>'  
select CAST(CONVERT(XML,@u,1) as NVARCHAR(50))  
```  
  
 Esse é o resultado:  
  
```  
<a a="  
    ????>">     
</a>  
```  
  
 Se não desejar aplicar a regra de proteção do último caractere em branco, você poderá usar a opção explícita 1 de CONVERT ao converter de **xml** em uma cadeia de caracteres ou em um tipo binário. Por exemplo, para evitar a definição de entidade, você pode fazer o seguinte:  
  
```  
select CONVERT(NVARCHAR(50), CONVERT(XML, '<a>   </a>', 1), 1)  
```  
  
 Observe que, o [Método query() (tipo de dados xml)](/sql/t-sql/xml/query-method-xml-data-type) resulta em uma instância de tipo de dados xml. Portanto qualquer resultado do método **query()** que seja convertido em um tipo de cadeia de caracteres ou binário tem a entidade definida de acordo com as regras descritas anteriormente. Para obter os valores da cadeia de caracteres que não têm a entidade definida, use o [Método value() (tipo de dados xml)](/sql/t-sql/xml/value-method-xml-data-type) . O seguinte é um exemplo de uso do método **query()** :  
  
```  
declare @x xml  
set @x = N'<a>This example contains an entitized char: <.</a>'  
select @x.query('/a/text()')  
```  
  
 Esse é o resultado:  
  
```  
This example contains an entitized char: <.  
```  
  
 O seguinte é um exemplo de uso do método **value()** :  
  
```  
select @x.value('(/a/text())[1]', 'nvarchar(100)')  
```  
  
 Esse é o resultado:  
  
```  
This example contains an entitized char: <.  
```  
  
## <a name="serializing-a-typed-xml-data-type"></a>Serializando um tipo de dados xml com tipo  
 Uma instância de tipo de dados **xml** com tipo contém valores com tipo de acordo com seus tipos de esquema XML. Esses valores são serializados de acordo com seu tipo de esquema XML no mesmo formato que a conversão de Xquery para procedimentos xs:string. Para obter mais informações, veja [Regras de conversão de tipo em XQuery](/sql/xquery/type-casting-rules-in-xquery).  
  
 Por exemplo, o valor de xs:double 1.34e1 é serializado como 13.4 conforme mostrado no exemplo a seguir:  
  
```  
declare @x xml  
set @x =''  
select CAST(@x.query('1.34e1') as nvarchar(50))  
```  
  
 Isso retorna o valor da cadeia de caracteres 13.4.  
  
## <a name="see-also"></a>Consulte também  
 [Regras de conversão de tipo em XQuery](/sql/xquery/type-casting-rules-in-xquery)   
 [CAST e CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)  
  
  
