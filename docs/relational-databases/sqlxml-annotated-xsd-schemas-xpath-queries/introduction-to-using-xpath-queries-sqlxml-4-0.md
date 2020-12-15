---
title: Introdução ao uso de consultas XPath (SQLXML)
description: Aprenda as noções básicas do uso de consultas XPath no SQLXML 4,0.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], about XPath queries
- W3C XPath specification
- XPath queries [SQLXML], functionality
ms.assetid: 01050a8e-0ccc-4a02-a4eb-b48be5c3f4f3
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2e69adfb9fcd75592f25595c70741864ba4493af
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414919"
---
# <a name="introduction-to-using-xpath-queries-sqlxml-40"></a>Introdução para usar consultas XPath (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Uma consulta de linguagem XPath pode ser especificada como parte de uma URL ou em um modelo. O esquema de mapeamento determina a estrutura desse fragmento resultante, e os valores são recuperados no banco de dados. Conceitualmente, esse processo é semelhante a criar exibições que usem a instrução CREATE VIEW e escrever consultas SQL com base nelas.  
  
> [!NOTE]  
>  Para entender as consultas XPath no SQLXML 4.0, é necessário estar familiarizado com as exibições XML e os conceitos relacionados, como modelos e esquemas de mapeamento. Para obter mais informações, consulte [introdução aos esquemas XSD anotados &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)e o padrão XPath definido pelo World Wide Web CONSORTIUM (W3C).  
  
 Um documento XML consiste em nós como, por exemplo, de elemento, de atributo, de texto etc. Por exemplo, considere este documento XML:  
  
```  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was  
          very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
```  
  
 Neste documento, **\<Customer>** é um nó de elemento, **CID** é um nó de atributo e **"importante"** é um nó de texto.  
  
 XPath é uma linguagem de navegação gráfica usada para selecionar um conjunto de nós em um documento XML. Cada operador de XPath seleciona um conjunto de nós com base em um conjunto selecionado por um operador de XPath anterior. Por exemplo, dado um conjunto de **\<Customer>** nós, o XPath pode selecionar todos os **\<Order>** nós com o valor de atributo de **Data** **"7/14/1999"**. O conjunto de nós resultante contém todos os pedidos com a data 14/7/1999.  
  
 XPath é definida pelo W3C como uma linguagem de navegação padrão. O SQLXML 4,0 implementa um subconjunto da especificação XPath do W3C, que está localizado em http://www.w3.org/TR/1999/PR-xpath-19991008.html .  
  
 Estas são as principais diferenças entre a implementação da XPath do W3C e a implementação do SQLXML 4.0.  
  
-   **Consultas raiz**  
  
     O SQLXML 4.0 não oferece suporte à consulta raiz (/). Cada consulta XPath deve começar em um nível superior **\<ElementType>** no esquema.  
  
-   **Relatando erros**  
  
     A especificação XPath do W3C não define nenhuma condição de erro. As consultas XPath que deixam de selecionar algum nó retornam um conjunto de nós vazio. No SQLXML 4.0, uma consulta pode retornar muitos tipos de mensagens de erro.  
  
-   **Ordem do documento**  
  
     No SQLXML 4.0, a ordem de documentos nem sempre é determinada. Portanto, predicados numéricos e eixos que usam a ordem de documento (como a **seguir**) não são implementados.  
  
     A ausência da ordem de documentos também significa que o valor da cadeia de caracteres de um nó só pode ser avaliado quando esse nó é mapeado para uma única coluna em uma única linha. Um elemento com elementos filho ou nós IDREFS ou NMTOKENS não pode ser convertido em cadeia de caracteres.  
  
    > [!NOTE]  
    >  Em alguns casos, a anotação de **campos de chave** ou as chaves da anotação de **relação** podem resultar em uma ordem de documento determinística. No entanto, esse não é o principal uso dessas anotações para obter mais informações, consulte [identificando colunas de chave usando SQL: campos-chave &#40;sqlxml 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md) e [especificando relações usando sql: relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md).  
  
-   **Tipos de dados**  
  
     O SQLXML 4,0 tem limitações na implementação da **cadeia de caracteres** XPath, **número** e tipos de dados **boolianos** . Para obter mais informações, consulte [tipos de dados XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md).  
  
-   **Consultas de vários produtos**  
  
     O SQLXML 4.0 não oferece suporte a consultas XPath de vários produtos como, por exemplo, `Customers[Order/@OrderDate=Order/@ShipDate]`. Essa consulta seleciona todos os clientes com um pedido qualquer em que OrderDate é igual a ShipDate de qualquer pedido.  
  
     No entanto, o SQLXML 4.0 oferece suporte a consultas como, por exemplo, `Customer[Order[@OrderDate=@ShippedDate]]`, que seleciona clientes com qualquer pedido em que OrderDate é igual a ShipDate.  
  
-   **Manipulação de erros e segurança**  
  
     Dependendo do esquema e da expressão de consulta XPath usados, os erros [!INCLUDE[tsql](../../includes/tsql-md.md)] podem ser expostos a usuários em determinadas condições.  
  
 As tabelas nas seguintes seções fornecem detalhes sobre como a implementação de consultas XPath no SQLXML 4.0 se diferencia da especificação do W3C nessas áreas.  
  
## <a name="supported-functionality"></a>Funcionalidade com suporte  
 A seguinte tabela mostra os recursos da linguagem XPath implementados no SQLXML 4.0.  
  
|Recurso|Item|Link para consultas de exemplo|  
|-------------|----------|----------------------------|  
|Eixos|**atributo**, **filho**, **pai** e **autoeixos**|[Especificando eixos em consultas XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-axes-in-xpath-queries-sqlxml-4-0.md)|  
|Predicados com valor booliano incluindo predicados sucessivos e aninhados||[Especificando operadores aritméticos em consultas XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Todos os operadores relacionais|=,! =, <, \<=, > , >=|[Especificando operadores relacionais em consultas XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-relational-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Operadores aritméticos|+, -, *, div|[Especificando operadores aritméticos em consultas XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Funções de conversão explícitas|**Number ()**, **String ()**, **booliano ()**|[Especificando funções de conversão explícitas em consultas XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-4-0.md)|  
|Operadores boolianos|AND, OR|[Especificando operadores boolianos em consultas XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-operators-in-xpath-queries-sqlxml-4-0.md)|  
|funções boolianas|**true ()**, **false ()**, **não ()**|[Especificando funções booleanas em consultas XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-functions-in-xpath-queries-sqlxml-4-0.md)|  
|Variáveis XPath||[Especificando variáveis XPath em consultas XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-xpath-variables-in-xpath-queries-sqlxml-4-0.md)|  
  
## <a name="unsupported-functionality"></a>Funcionalidade sem suporte  
 A seguinte tabela mostra os recursos da linguagem XPath não implementados no SQLXML 4.0.  
  
|Recurso|Item|  
|-------------|----------|  
|Eixos|**ancestral**, **ancestral ou próprio**, **descendente**, **descendente ou próprio (//)**, **seguinte**, **irmão seguinte**, **namespace**, **precedente**, **irmão precedente**|  
|Predicados de valor numérico||  
|Operadores aritméticos|mod|  
|Funções de nó|**ancestral**, **ancestral ou próprio**, **descendente**, **descendente ou próprio (//)**, **seguinte**, **irmão seguinte**, **namespace**, **precedente**, **irmão precedente**|  
|Funções de cadeia de caracteres|**String ()**, **concat ()**, **começa com ()**, **Contains ()**, **substring-Before ()**, **substring-after ()**, **substring ()**, **String-Length ()**, **Normalize ()**, **translate ()**|  
|funções boolianas|**lang ()**|  
|Funções numéricas|**Sum ()**, **Floor ()**, **teto ()**, **Round ()**|  
|operador Union|&#124;|  
  
 Ao especificar consultas XPath em um modelo, observe o seguinte comportamento:  
  
-   O XPath pode conter caracteres como < ou & com significados especiais em XML (e o modelo é um documento XML). Você deve escapar esses caracteres usando a codificação de & XML ou especificar o XPath na URL.  
  
## <a name="see-also"></a>Consulte Também  
 [Usando consultas XPath no SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
  
  
