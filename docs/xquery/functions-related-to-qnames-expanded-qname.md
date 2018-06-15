---
title: Expanded-QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b76f85fae2f01322838c40b79227da896fabd01c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33077763"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>Funções relacionadas a QNames - expanded-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna um valor do tipo xs: QName com o namespace URI especificado no *$paramURI* e o nome do local especificado no *$paramLocal*. Se *$paramURI* é a cadeia de caracteres vazia ou a sequência vazia, ele não representará um namespace.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$paramURI*  
 É o namespace URI para o QName.  
  
 *$paramLocal*  
 É a parte do nome local do QName.  
  
## <a name="remarks"></a>Remarks  
 O seguinte se aplica ao **expanded-QName()** função:  
  
-   Se o *$paramLocal* valor especificado não está na forma léxica correta do tipo xs: NCName, a sequência vazia será retornada e representa um erro dinâmico.  
  
-   Não é oferecido suporte à conversão do tipo xs:QName em qualquer outro tipo no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por isso, o **expanded-QName()** função não pode ser usada na construção XML. Por exemplo, quando você estiver construindo um nó, como `<e> expanded-QName(…) </e>`, o valor precisa ser não digitado. Isso exigiria que você convertesse o valor de tipo xs:QName retornado por `expanded-QName()` para xdt:untypedAtomic. Porém, não é oferecido suporte para isso. Em um exemplo posterior neste tópico é oferecida uma solução.  
  
-   Você pode modificar ou comparar os valores de tipo QName existentes. Por exemplo, `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` compara o valor do elemento, <`e`>, com o QName retornado pelo **expanded-QName()** função.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML que são armazenados em várias **xml** colunas de tipo de [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. Substituindo um valor de nó do tipo QName  
 Este exemplo ilustra como você pode modificar o valor de um nó de elemento do tipo QName. O exemplo executa o seguinte:  
  
-   Cria uma coleção de esquemas XML que define um elemento do tipo QName.  
  
-   Cria uma tabela com um **xml** coluna de tipo por meio da coleção de esquema XML.  
  
-   Salva uma instância XML na tabela.  
  
-   Usa o **Modify ()** método do tipo de dados xml para modificar o valor do elemento de tipo QName na instância. O **expanded-QName()** função é usada para gerar o novo valor do tipo QName.  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 Na consulta a seguir, o <`ElemQN`> o valor do elemento é substituído usando o **Modify ()** método de tipo de dados xml e o valor de substituição do XML DML, como mostrado.  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("http://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 Este é o resultado. Observe que o elemento <`ElemQN`> do tipo QName agora tem um novo valor:  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="http://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 As instruções a seguir removem os objetos usados no exemplo.  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>B. Tratando as limitações ao usar a função expanded-QName()  
 O **expanded-QName** função não pode ser usada na construção XML. O exemplo a seguir ilustra isto. Para solucionar essa limitação, o exemplo primeiro insere um nó e, em seguida, modifica o nó.  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="http://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 A tentativa a seguir adiciona outro elemento <`root`> mas falha, pois não há suporte para a função expanded-QName() na construção XML.  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 Uma solução para isso é primeiro inserir uma instância com um valor para o elemento <`root`> e, em seguida, modificá-lo. Neste exemplo, um valor inicial nulo é usado quando o elemento <`root`> é inserido. A coleção de esquemas XML neste exemplo permite um valor nulo para o elemento <`root`>.  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="http://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 Você pode comparar o valor QName, como mostrado na consulta a seguir. A consulta retorna somente o <`root`> cujos valores correspondem QName de elementos de tipo de valor retornado pelo **expanded-QName()** função.  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Há uma limitação: O **expanded-QName()** função aceita a sequência vazia como o segundo argumento e retorna vazia em vez de gerar um erro de tempo de execução quando o segundo argumento é incorreto.  
  
## <a name="see-also"></a>Consulte também  
 [Funções relacionadas a QNames &#40;XQuery&#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
