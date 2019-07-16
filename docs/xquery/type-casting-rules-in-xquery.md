---
title: Tipo de regras de conversão em XQuery | Microsoft Docs
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
- XQuery, type casting
- casting rules [XML in SQL Server]
- explicit casting [SQL Server]
- type casting rules [XML in SQL Server]
- cast as operator
- implicit casting
ms.assetid: f2e91306-2b1b-4e1c-b6d8-a34fb9980057
author: rothja
ms.author: jroth
ms.openlocfilehash: a8372e5079b79cc694ccf51f1b6f7cddcf0fed43
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946211"
---
# <a name="type-casting-rules-in-xquery"></a>Regras de conversão de tipos em XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  O diagrama de especificações de funções e operadores do W3C XQuery 1.0 e do XPath 2.0 mostra os tipos de dados internos. Isso inclui os tipos derivados e primitivos internos.  
  
 ![Hierarquia de tipo XQuery 1.0](../xquery/media/xquery-typing-rules.gif "hierarquia de tipo XQuery 1.0")  
  
 Este tópico descreve as regras de conversão de tipos aplicadas à conversão de um tipo em outro usando um dos seguintes métodos:  
  
-   Conversão explícita que você faz usando **convertido** ou as funções do construtor de tipo (por exemplo, `xs:integer("5")`).  
  
-   Conversão implícita que ocorre durante a promoção de tipos  
  
## <a name="explicit-casting"></a>Conversão explícita  
 A tabela a seguir descreve a conversão de tipos permitida entre os tipos primitivos internos.  
  
 ![Descreve as regras de conversão para XQuery. ](../xquery/media/casting-builtin-types.gif "Descreve as regras de conversão para XQuery.")  
  
-   Um tipo primitivo interno pode ser convertido em outro tipo primitivo interno, com base nas regras na tabela.  
  
-   Um tipo primitivo pode ser convertido em qualquer tipo derivado desse tipo primitivo. Por exemplo, você pode converter de **xs: decimal** à **xs: Integer**, ou de **xs: decimal** para **xs: Long**.  
  
-   Um tipo derivado pode ser convertido em qualquer tipo que seja seu ancestral na hierarquia de tipo, todo o caminho até o seu tipo base primitivo interno. Por exemplo, você pode converter de **xs: token** à **xs: normalizedstring** ou a **xs: string**.  
  
-   Um tipo derivado poderá ser convertido em um tipo primitivo se seu ancestral primitivo puder ser convertido no tipo de destino. Por exemplo, você pode converter **xs: Integer**, um tipo derivado, em um **xs: string**, primitivos de tipo, porque **xs: decimal**, **xs: Integer**do o ancestral primitivo, pode ser convertido em **xs: string**.  
  
-   Um tipo derivado pode ser convertido em outro tipo derivado se o ancestral primitivo do tipo de origem puder ser convertido no ancestral primitivo do tipo de destino. Por exemplo, você pode converter de **xs: Integer** à **xs: token**, pois você pode converter de **xs: decimal** para **xs: string**.  
  
-   As regras de conversão de tipos definidos pelo usuário em tipos internos são as mesmas para os tipos internos. Por exemplo, você pode definir um **myInteger** tipo derivado de **xs: Integer** tipo. Em seguida, **myInteger** pode ser convertido em **xs: token**, pois **xs: decimal** pode ser convertido em **xs: string**.  
  
 Não há suporte para os seguintes tipos de conversão:  
  
-   Não é permitida a conversão em ou de tipos de lista. Isso inclui tipos de lista definidos pelo usuário e tipos de listas internos, como **xs: IDREFS**, **xs: Entities**, e **xs: NMTOKENS**.  
  
-   Conversão em ou de **xs: QName** não tem suporte.  
  
-   **xs: Notation** e os subtipos completamente ordenados de duração, **XDT: yearmonthduration** e **XDT: daytimeduration**, não têm suporte. Consequentemente, não há suporte para conversão em ou desses tipos.  
  
 Os exemplos a seguir ilustram a conversão de tipo explícito.  
  
### <a name="example-a"></a>Exemplo A  
 O exemplo a seguir consulta uma variável de tipo xml. A consulta retorna uma sequência de um valor de tipo simples digitada como xs:string.  
  
```  
declare @x xml  
set @x = '<e>1</e><e>2</e>'  
select @x.query('/e[1] cast as xs:string?')  
go  
```  
  
### <a name="example-b"></a>Exemplo B  
 O exemplo a seguir consulta uma variável xml digitada. O exemplo cria primeiro uma coleção de esquemas XML. Em seguida, utiliza a coleção de esquemas XML para criar uma variável xml digitada. O esquema fornece as informações de digitação para a instância XML atribuída à variável. São, então, especificadas consultas na variável.  
  
```  
create xml schema collection myCollection as N'  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">  
      <xs:element name="root">  
            <xs:complexType>  
                  <xs:sequence>  
                        <xs:element name="A" type="xs:string"/>  
                        <xs:element name="B" type="xs:string"/>  
                        <xs:element name="C" type="xs:string"/>  
                  </xs:sequence>  
            </xs:complexType>  
      </xs:element>  
</xs:schema>'  
go  
```  
  
 A consulta a seguir retorna um erro estático, porque você não sabe quantos superiores <`root`> elementos estão na instância do documento.  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
          <root><A>4</A><B>5</B><C>6</baz></C>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
 Especificando um singleton <`root`> elemento na expressão, a consulta for bem-sucedida. A consulta retorna uma sequência de um valor de tipo simples digitada como xs:string.  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
select @x.query('/root[1]/A cast as xs:string?')  
go  
```  
  
 No exemplo a seguir, a variável de tipo xml inclui uma palavra-chave de documento que especifica a coleção de esquemas XML. Isso indica que a instância XML deve ser um documento que tenha um único elemento de nível superior. Se você criar dois <`root`> elementos na instância XML, ele retornará um erro.  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
go  
```  
  
 Você pode alterar a instância para incluir apenas um elemento de nível superior. Dessa forma, a consulta funcionará. Novamente, a consulta retorna uma sequência de um valor de tipo simples digitado como xs:string.  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
## <a name="implicit-casting"></a>Conversão implícita  
 A conversão implícita só é permitida para tipos numéricos e tipos atômicos não digitados. Por exemplo, a seguinte **min ()** função retorna o mínimo dos dois valores:  
  
```  
min(xs:integer("1"), xs:double("1.1"))  
```  
  
 Neste exemplo, os dois valores passados em XQuery **min ()** função são de tipos diferentes. Portanto, a conversão implícita é executada em que **inteiro** tipo é promovido a **duplo** e as duas **double** valores são comparados.  
  
 A promoção de tipo como descrita nesse exemplo segue estas regras:  
  
-   Um tipo numérico derivado interno pode ser promovido a seu tipo básico. Por exemplo, **inteiro** pode ser promovido a **decimal**.  
  
-   Um **decimais** pode ser promovido a **float,** e um **float** pode ser promovido a **double**.  
  
 Como a conversão implícita só é permitida para tipos numéricos, o seguinte não é permitido:  
  
-   Conversão implícita para tipos de cadeia de caracteres. Por exemplo, se duas **cadeia de caracteres** tipos são esperados e passar em um **cadeia de caracteres** e um **token**, nenhuma conversão implícita ocorrerá e um erro será retornado.  
  
-   Conversão implícita de tipos numéricos em tipos de cadeia de caracteres. Por exemplo, se você passar um valor do tipo inteiro em uma função que está esperando um parâmetro de tipo de cadeia de caracteres, nenhuma conversão implícita ocorrerá e um erro será retornado.  
  
## <a name="casting-values"></a>Convertendo valores  
 Ao converter de um tipo a outro, os valores reais são transformados do espaço de valor do tipo de origem no espaço de valor do tipo de destino. Por exemplo, a conversão de um xs:decimal em um xs:double transformará o valor decimal em um valor duplo.  
  
 A seguir são apresentadas algumas das regras de transformação.  
  
##### <a name="casting-a-value-from-a-string-or-untypedatomic-type"></a>Convertendo um valor de um tipo de cadeia de caracteres ou untypedAtomic  
 O valor que está sendo convertido em um tipo de cadeia de caracteres ou untypedAtomic é transformado da mesma maneira que a validação do valor com base nas regras do tipo de destino. Isso inclui as regras de processamento de espaço em branco e padrão eventual. Por exemplo, o apresentado a seguir terá êxito e gerará um valor duplo, 1.1e0:  
  
 `xs:double("1.1")`  
  
 Na conversão em tipos binários, como xs:base64Binary ou xs:hexBinary, de um tipo de cadeia de caracteres ou untypedAtomic, os valores de entrada precisam ser codificados como base64 ou hex, respectivamente.  
  
##### <a name="casting-a-value-to-a-string-or-untypedatomic-type"></a>Convertendo um valor em um tipo de cadeia de caracteres ou untypedAtomic  
 A conversão em um tipo de cadeia de caracteres ou untypedAtomic transforma o valor em sua representação léxica canônica do XQuery. Especificamente, isso pode significar que um valor que pode ter obedecido a um padrão específico ou outra restrição durante a entrada não será representado de acordo com essa restrição.  Para informar os usuários sobre isso, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sinaliza os tipos em que a restrição de tipo pode ser um problema, fornecendo um aviso quando esses tipos são carregados na coleção de esquemas.  
  
 Ao converter um valor do tipo xs:float ou xs:double, ou qualquer um de seus subtipos, em um tipo de cadeia de caracteres ou untypedAtomic, o valor será representado em notação científica. Isso só é realizado quando o valor absoluto do valor é inferior a 1.0E-6, ou superior ou igual a 1.0E6. Isso significa que 0 é serializado em notação científica para 0.0E0.  
  
 Por exemplo, `xs:string(1.11e1)` retornará o valor da cadeia de caracteres `"11.1"`, enquanto `xs:string(-0.00000000002e0)` retornará o valor da cadeia de caracteres, `"-2.0E-11"`.  
  
 Na conversão de tipos binários, como xs:base64Binary ou xs:hexBinary, em um tipo de cadeia de caracteres ou untypedAtomic, os valores binários serão representados em sua forma codificada base64 ou hex, respectivamente.  
  
##### <a name="casting-a-value-to-a-numeric-type"></a>Convertendo um valor em um tipo numérico  
 Na conversão de um valor de um tipo numérico em um valor de outro tipo numérico, o valor é mapeado de um espaço de valor para outro sem passar pela serialização da cadeia de caracteres. Se o valor não atender à restrição de um tipo de destino, as seguintes regras serão aplicadas:  
  
-   Se o valor de origem já for numérico e o tipo de destino for xs:float ou um subtipo que permita valores -INF ou INF e a conversão do valor numérico de origem resultar em um estouro, o valor será mapeado para INF se o valor for positivo ou -INF se o valor for negativo. Se o tipo de destino não permitir INF ou -INF e ocorrer um estouro, haverá falha na conversão e o resultado nessa versão do SQL Server será a sequência vazia.  
  
-   Se o valor de origem já for numérico e o tipo de destino for um tipo numérico, que inclui 0, -0e0 ou 0e0 em seu intervalo de valores aceito, e a conversão do valor numérico de destino resultar em um estouro, o valor será mapeado das seguintes formas:  
  
    -   O valor será mapeado para 0 para um tipo de destino decimal.  
  
    -   O valor será mapeado para -0e0 quando o valor for um estouro negativo.  
  
    -   O valor será mapeado para 0e0 quando o valor for um estouro negativo positivo para um tipo de destino flutuante ou duplo.  
  
     Se o tipo de destino não incluir zero em seu espaço de valor, haverá falha na conversão e o resultado será a sequência vazia.  
  
     Observe que essa conversão de um valor em um tipo binário de ponto flutuante, como xs:float, xs:double ou qualquer um dos subtipos, poderá perder precisão.  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   Não há suporte para o valor do ponto flutuante NaN.  
  
-   Os valores conversíveis são restritos pelas restrições de implementação de tipos designadas. Por exemplo, você não pode converter uma cadeia de caracteres de data com um ano negativo em **xs: Date**. Tal conversão resultará em uma sequência vazia se o valor for fornecido em tempo de execução (em vez de gerar um erro de tempo de execução).  
  
## <a name="see-also"></a>Consulte também  
 [Definir a serialização de dados XML](../relational-databases/xml/define-the-serialization-of-xml-data.md)  
  
  
