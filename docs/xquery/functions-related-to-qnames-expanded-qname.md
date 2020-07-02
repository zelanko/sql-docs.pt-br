---
title: expanded-QName (XQuery) | Microsoft Docs
description: Saiba como usar a função expanded-QName () para retornar o URI do namespace e a parte do nome local de um QName.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
author: rothja
ms.author: jroth
ms.openlocfilehash: 88bbf5697112fd80f8ffea629a1ad2b9e99977fa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720046"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>Funções Relacionadas a QNames – expanded-QName
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Retorna um valor do tipo xs: QName com o URI do namespace especificado no *$paramURI* e o nome local especificado na *$paramLocal*. Se *$paramURI* for a cadeia de caracteres vazia ou a sequência vazia, ela não representará nenhum namespace.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$paramURI*  
 É o namespace URI para o QName.  
  
 *$paramLocal*  
 É a parte do nome local do QName.  
  
## <a name="remarks"></a>Comentários  
 O seguinte se aplica à função **expanded-QName ()** :  
  
-   Se o valor de *$paramLocal* especificado não estiver no formato léxico correto para o tipo xs: NCName, a sequência vazia será retornada e representará um erro dinâmico.  
  
-   Não é oferecido suporte à conversão do tipo xs:QName em qualquer outro tipo no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por isso, a função **expanded-QName ()** não pode ser usada na construção XML. Por exemplo, quando você estiver construindo um nó, como `<e> expanded-QName(...) </e>`, o valor precisa ser não digitado. Isso exigiria que você convertesse o valor de tipo xs:QName retornado por `expanded-QName()` para xdt:untypedAtomic. Porém, não é oferecido suporte para isso. Em um exemplo posterior neste tópico é oferecida uma solução.  
  
-   Você pode modificar ou comparar os valores de tipo QName existentes. Por exemplo, `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` compara o valor do elemento, <`e`>, com QName retornado pela função **expanded-QName ()** .  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-replacing-a-qname-type-node-value"></a>a. Substituindo um valor de nó do tipo QName  
 Este exemplo ilustra como você pode modificar o valor de um nó de elemento do tipo QName. O exemplo executa o seguinte:  
  
-   Cria uma coleção de esquemas XML que define um elemento do tipo QName.  
  
-   Cria uma tabela com uma coluna de tipo **XML** usando a coleção de esquema XML.  
  
-   Salva uma instância XML na tabela.  
  
-   Usa o método **Modify ()** do tipo de dados XML para modificar o valor do elemento tipo QName na instância. A função **expanded-QName ()** é usada para gerar o novo valor de tipo QName.  
  
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
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 Na consulta a seguir, o `ElemQN` valor do elemento <> é substituído usando o método **Modify ()** do tipo de dados XML e o valor de Replace de XML DML, conforme mostrado.  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("https://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 Este é o resultado. Observe que o elemento <`ElemQN`> do tipo QName agora tem um novo valor:  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="https://myURI">p1:myLocalName</ElemQN>  
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
 A função **expanded-QName** não pode ser usada na construção XML. O exemplo a seguir ilustra isto. Para solucionar essa limitação, o exemplo primeiro insere um nó e, em seguida, modifica o nó.  
  
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
insert into T values ('<root xmlns:a="https://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 A tentativa a seguir adiciona outro <`root` elemento>, mas falha, porque a função expanded-QName () não tem suporte na construção XML.  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 Uma solução para isso é primeiro inserir uma instância com um valor para o elemento <`root`> e, em seguida, modificá-la. Neste exemplo, um valor inicial nil é usado quando o elemento <`root`> é inserido. A coleção de esquema XML neste exemplo permite um valor nil para o `root` elemento <>.  
  
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
  
 `<root xmlns:a="https://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 Você pode comparar o valor QName, como mostrado na consulta a seguir. A consulta retorna apenas os `root` elementos <> cujos valores correspondem ao valor do tipo QName retornado pela função **expanded-QName ()** .  
  
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
 Há uma limitação: a função **expanded-QName ()** aceita a sequência vazia como o segundo argumento e retornará vazio em vez de gerar um erro em tempo de execução quando o segundo argumento estiver incorreto.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções relacionadas a QNames &#40;&#41;XQuery](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
