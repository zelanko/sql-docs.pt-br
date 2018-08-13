---
title: Usando sequências de Escape do SQL | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 00f9e25a-088e-4ac6-aa75-43eacace8f03
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b039367f418049fabde25cda26dedde8939ab741
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662288"
---
# <a name="using-sql-escape-sequences"></a>Usando sequências de escape do SQL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte ao uso de sequências de escape do SQL, conforme definido pela API do JDBC. As sequências de escape são usadas em uma instrução SQL para informar ao driver que a parte de escape da cadeia de caracteres SQL deve ser tratada de forma diferente. Quando o driver JDBC processa a parte de escape de uma cadeia de caracteres SQL, ele converte essa parte da cadeia de caracteres em código SQL que o SQL Server entende.  
  
 Há cinco tipos de sequências de escape requeridas pela API JDBC e todos têm o suporte do driver JDBC:  
  
- Literais do curinga LIKE
- Manipulação de função
- Literais de data e hora
- Chamadas de procedimento armazenado
- Junções externas
- Sintaxe de escape de limite

A sintaxe da sequência de escape usada pelo driver JDBC é a seguinte:  
  
`{keyword ...parameters...}`  
  
> [!NOTE]  
> O processamento de escape do SQL sempre está ativado para o driver JDBC.  
  
As seções a seguir descrevem os cinco tipos de sequências de escape e como elas têm o suporte do driver JDBC.  
  
## <a name="like-wildcard-literals"></a>Literais do curinga LIKE

O driver JDBC é compatível com a sintaxe `{escape 'escape character'}` para uso de curingas da cláusula LIKE como literais. Por exemplo, o código a seguir retornará valores para col3, onde o valor de col2 começa literalmente com um sublinhado (e não seu uso de curinga).  

```java
ResultSet rst = stmt.executeQuery("SELECT col3 FROM test1 WHERE col2   
LIKE '\\_%' {escape '\\'}");  
```

> [!NOTE]  
> A sequência de escape deve estar no fim da instrução SQL. Para várias instruções SQL em uma cadeia de caracteres de comando, a sequência de escape precisa estar no fim de cada instrução SQL pertinente.  

## <a name="function-handling"></a>Manipulação de função

O driver JDBC dá suporte às sequências de escape de função em instruções SQL com a seguinte sintaxe:  

```sql
{fn functionName}  
```

em que `functionName` é uma função compatível com o driver JDBC. Por exemplo: 

```sql
SELECT {fn UCASE(Name)} FROM Employee  
```

A tabela a seguir lista as várias funções que têm o suporte do driver JDBC ao usar uma sequência de escape de função:  
  
| Funções de cadeia de caracteres                                                                                                                                                                                                                                                                                                                        | Funções numéricas                                                                                                                                                                                                                                                                                                                                                                                                   | Funções de data e hora                                                                                                                                                                                                                                                                                                                                             | Funções de sistema                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| ASCII<br /><br /> CHAR<br /><br /> CONCAT<br /><br /> DIFFERENCE<br /><br /> INSERT<br /><br /> LCASE<br /><br /> LEFT<br /><br /> LENGTH<br /><br /> LOCATE<br /><br /> LTRIM<br /><br /> REPEAT<br /><br /> REPLACE<br /><br /> RIGHT<br /><br /> RTRIM<br /><br /> SOUNDEX<br /><br /> SPACE<br /><br /> SUBSTRING<br /><br /> UCASE | ABS<br /><br /> ACOS<br /><br /> ASIN<br /><br /> ATAN<br /><br /> ATAN2<br /><br /> CEILING<br /><br /> COS<br /><br /> COT<br /><br /> DEGREES<br /><br /> EXP<br /><br /> FLOOR<br /><br /> LOG<br /><br /> LOG10<br /><br /> MOD<br /><br /> PI<br /><br /> POWER<br /><br /> RADIANS<br /><br /> RAND<br /><br /> ROUND<br /><br /> SIGN<br /><br /> SIN<br /><br /> SQRT<br /><br /> TAN<br /><br /> TRUNCATE | CURDATE<br /><br /> CURTIME<br /><br /> DAYNAME<br /><br /> DAYOFMONTH<br /><br /> DAYOFWEEK<br /><br /> DAYOFYEAR<br /><br /> EXTRACT<br /><br /> HOUR<br /><br /> MINUTE<br /><br /> MONTH<br /><br /> MONTHNAME<br /><br /> NOW<br /><br /> QUARTER<br /><br /> SECOND<br /><br /> TIMESTAMPADD<br /><br /> TIMESTAMPDIFF<br /><br /> WEEK<br /><br /> YEAR | DATABASE<br /><br /> IFNULL<br /><br /> Usuário |

> [!NOTE]  
> Se você tentar usar uma função que não tenha o suporte do banco de dados, ocorrerá um erro.  

## <a name="date-and-time-literals"></a>Literais de data e hora

A sintaxe de escape para data, hora e literais de carimbo de data/hora é a seguinte:  

```sql
{literal-type 'value'}  
```

em que `literal-type` é um dos seguintes:  
  
| Tipo de literal | Descrição | Formato do valor               |
| ------------ | ----------- | -------------------------- |
| d            | data        | aaaa-mm-dd                 |
| t            | Hora        | hh:mm:ss [1]               |
| ts           | TimeStamp   | aaaa-mm-dd hh:mm:ss[.f...] |
  
Por exemplo:  

```sql
UPDATE Orders SET OpenDate={d '2005-01-31'}
WHERE OrderID=1025  
```

## <a name="stored-procedure-calls"></a>Chamadas de procedimento armazenado

O driver JDBC é compatível com as sintaxes de escape `{? = call proc_name(?,...)}` e `{call proc_name(?,...)}` para chamadas de procedimento armazenado, dependendo da necessidade de processar um parâmetro de retorno.  
  
Um procedimento é um objeto executável armazenado no banco de dados. Em geral, é uma ou mais instruções SQL que foram pré-compiladas. A sintaxe da sequência de escape para chamar um procedimento armazenado é a seguinte:  

```sql
{[?=]call procedure-name[([parameter][,[parameter]]...)]}  
```

em que `procedure-name` especifica o nome de um procedimento armazenado e `parameter` especifica um parâmetro de procedimento armazenado.  
  
Para obter mais informações sobre como usar o `call` sequência com procedimentos armazenados de escape, consulte [usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md).  

## <a name="outer-joins"></a>Junções externas

O driver JDBC dá suporte à sintaxe de junção externa esquerda, direita e completa do SQL92. A sequência de escape de junções externas é a seguinte:  

```sql
{oj outer-join}  
```

onde outer-join é:  

```sql
table-reference {LEFT | RIGHT | FULL} OUTER JOIN
{table-reference | outer-join} ON search-condition  
```

em que `table-reference` é um nome de tabela e `search-condition` é a condição de junção que você deseja usar para as tabelas.  
  
Por exemplo:  

```sql
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status
   FROM {oj Customers LEFT OUTER JOIN
      Orders ON Customers.CustID=Orders.CustID}
   WHERE Orders.Status='OPEN'  
```

As seguintes sequências de escape de junção externa têm o suporte do driver JDBC:  

- Junções externas esquerdas
- Junções externas direitas
- Junções externas completas
- Junções externas aninhadas

## <a name="limit-escape-syntax"></a>Sintaxe de escape de limite  

> [!NOTE]  
> A sintaxe de escape LIMIT só tem suporte pelo Microsoft JDBC Driver 4.2 (ou superior) for SQL Server ao usar JDBC 4.1 ou superior.  
  
 A sintaxe de escape LIMIT é da seguinte maneira:  

```sql
LIMIT <rows> [OFFSET <row offset>]  
```

A sintaxe de escape tem duas partes: \<*rows*> é obrigatória e especifica o número de linhas a serem retornadas. OFFSET e \<*deslocamento da linha*> são opcionais e especificam o número de linhas a serem ignoradas antes de começar a retornar linhas. O driver JDBC dá suporte apenas à parte obrigatória, transformando a consulta para usar TOP em vez de LIMIT. O SQL Server não d suporte à cláusula LIMIT. **O driver JDBC não dá suporte opcional \<deslocamento da linha> e o driver gerará uma exceção se for usado**.  
  
## <a name="see-also"></a>Consulte Também

[Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
