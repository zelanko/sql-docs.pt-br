---
title: Compreendendo as conversões de tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7029faf333c00fc18e4f35743706a012b76c1e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004179"
---
# <a name="understanding-data-type-conversions"></a>Entendendo conversões de tipo de dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para facilitar a conversão de tipos de dados da linguagem de programação Java em tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece conversões de tipo de dados, conforme exigido pela especificação de JDBC. Para flexibilidade adicional, todos os tipos são conversíveis de e para tipos de dados **Object**, **String**e **byte []** .

## <a name="getter-method-conversions"></a>Conversões de método getter

Com base nos tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o gráfico seguinte contém o mapa de conversão do driver JDBC para os métodos get\<Type>() da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) e as conversões com suporte para os métodos get\<Type> da classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).

![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")

Há três categorias de conversões que têm suporte pelos métodos getter do driver JDBC:

- **Sem perda (x)** : conversões para casos em que o tipo de elemento é o mesmo ou menor do que o tipo getter subjacente. Por exemplo, ao chamar getBigDecimal em uma coluna decimal do servidor subjacente, nenhuma conversão é necessária.

- **Convertida (y)** : conversões de tipos de servidor numéricos para tipos de linguagem Java em que a conversão é normal e segue as regras de conversão da linguagem Java. Para estas conversões, a precisão é sempre truncada, nunca arredondada, e o estouro é tratado como módulo do tipo de destino, que é menor. Por exemplo, chamar getInt em uma coluna **decimal** subjacente que contém "1,9999" retornará "1", ou se o valor **decimal** subjacente for "3000000000", o valor **int** estourará "-1294967296".

- **Dependente de dados (z)** : conversões de tipos de caracteres subjacentes para tipos numéricos exigem que os tipos de caracteres contenham valores que possam ser convertidos em tipo. Nenhuma outra conversão é realizada. Se o valor for muito grande para o tipo getter, o valor não será válido. Por exemplo, se getInt for chamado em uma coluna de varchar(50) que contém "53", o valor será retornado como um **int**; mas se o valor subjacente for "xyz" ou "3000000000", um erro será lançado.

Se GetString for chamado em um tipo de dados **binário**, **varbinary**, **varbinary (max)** ou de coluna de **imagem** , o valor será retornado como um valor de cadeia de caracteres hexadecimal.

## <a name="updater-method-conversions"></a>Conversões de método updater

Para os dados de tipo Java passados para os métodos \<Type>() da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), as conversões a seguir se aplicam.

![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")

Há três categorias de conversões que têm suporte pelos métodos updater do driver JDBC:

- **Sem perda (x)** : conversões para casos em que o tipo de elemento é o mesmo ou menor do que o tipo updater subjacente. Por exemplo, ao chamar updateBigDecimal em uma coluna decimal do servidor subjacente, nenhuma conversão é necessária.

- **Convertida (y)** : conversões de tipos de servidor numéricos para tipos de linguagem Java em que a conversão é normal e segue as regras de conversão da linguagem Java. Para estas conversões, a precisão é sempre truncada (nunca arredondada) e o estouro é tratado como módulo do tipo de destino (menor). Por exemplo, chamar updateDecimal em uma coluna **int** subjacente que contém "1,9999" retornará "1", ou se o valor **decimal** subjacente for "3000000000", o valor **int** estourará "-1294967296".

- **Dependente de dados (z)** : conversões de tipos de dados de origem subjacentes em tipos de dados de destino que exigem que os valores contidos possam ser convertidos em tipos de destino. Conversões de tipos de dados de origem subjacentes em tipos de dados de destino que exigem que os valores contidos possam ser convertidos em tipos de destino. Nenhuma outra conversão é realizada. Se o valor for muito grande para o tipo getter, o valor não será válido. Por exemplo, se updateString for chamado em uma coluna int que contém "53", a atualização será bem-sucedida; mas se o valor subjacente de String for "foo" ou "3000000000", um erro será lançado.

Quando updateString é chamado em um tipo de dados **Binary**, **varbinary**, **varbinary (max)** ou **Image** Column, ele manipula o valor da cadeia de caracteres como um valor de cadeia de caracteres hexadecimal.

Quando o tipo de dados da coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for **XML**, o valor de dados deverá ser um **XML** válido. Ao chamar os métodos updateBytes, updateBinaryStream ou updateBlob, o valor de dados deve ser a representação de cadeia de caracteres hexadecimal dos caracteres XML. Por exemplo:

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Observe que uma marca de ordem de byte (BOM) é exigida se os caracteres XML estiverem em codificações de caracteres específicas.

## <a name="setter-method-conversions"></a>Conversões de método setter

Para os dados de tipo Java passados para os métodos set\<Type>() da classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e da classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), as conversões a seguir se aplicam.

![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")

O servidor experimenta qualquer conversão e retorna erros quando há falha.

No caso do tipo de dados **String** , se o valor exceder o comprimento de **varchar**, ele será mapeado para **LONGVARCHAR**. Da mesma forma, **nvarchar** mapeia para **LONGNVARCHAR** se o valor excede o comprimento com suporte de **nvarchar**. O mesmo é válido para **byte[]** . Valores maiores que **varbinary** se tornam **LONGVARBINARY**.

Há duas categorias de conversões que têm suporte pelos métodos setter do driver JDBC:

- **Sem perda (x)** : conversões para casos numéricos em que o tipo setter é o mesmo ou menor do que o tipo de servidor subjacente. Por exemplo, ao chamar setBigDecimal em uma coluna **decimal** do servidor subjacente, nenhuma conversão é necessária. Para casos de numérico para caractere, o tipo de dados Java **numeric** é convertido para uma **String**. Por exemplo, chamar setDouble com um valor de "53" em uma coluna de varchar (50) gera um valor de caractere "53" na coluna de destino.

- **Convertido (y)** : conversões de um tipo **numérico** de Java para um tipo **numérico** de servidor subjacente menor. Esta conversão é normal e segue as convenções de conversão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A precisão sempre é truncada (nunca arredondada) e o estouro lança um erro de conversão sem suporte. Por exemplo, usar updateDecimal com um valor de "1.9999" em uma coluna de inteiro subjacente resulta em um "1" na coluna de destino; mas se for passado "3000000000", o driver lançará um erro.

- **Dependente de dados (z)** : conversões de um tipo **de cadeia de caracteres** Java [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o tipo de dados subjacente depende das seguintes condições: o driver envia o valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da **cadeia de caracteres** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executa conversões, se necessário. Se a sendStringParametersAsUnicode for definida como true e o tipo de dados subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for **imagem**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permitirá converter **nvarchar** em **imagem** e gerará um SQLServerException. Se sendStringParametersAsUnicode for definido como false e o tipo de dados subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for  **a imagem**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permitirá a conversão de **varchar** em **imagem** e não gerará uma exceção.

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza as conversões e passa os erros de volta para o driver JDBC quando há problemas.

Quando o tipo de dados da coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for **XML**, o valor de dados deverá ser um **XML** válido. Ao chamar os métodos updateBytes, updateBinaryStream ou updateBlob, o valor de dados deve ser a representação de cadeia de caracteres hexadecimal dos caracteres XML. Por exemplo:

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Observe que uma marca de ordem de byte (BOM) é exigida se os caracteres XML estiverem em codificações de caracteres específicas.

## <a name="conversions-on-setobject"></a>Conversões em setObject

> [!NOTE]  
> Os drivers JDBC da Microsoft 4,2 (e superiores) para SQL Server dão suporte a JDBC 4,1 e 4,2. Para obter mais detalhes sobre mapeamentos e conversões de tipo de dados 4,1 e 4,2, consulte [conformidade do jdbc 4,1 para o driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e conformidade com o [JDBC 4,2 para o driver JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md), além das informações abaixo.

Para os dados de tipo Java passados para os métodos setObject(\<Type>) da classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), as conversões a seguir se aplicam.

![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")

O método setObject sem tipo designado especificado usa o mapeamento padrão. No caso do tipo de dados **String** , se o valor exceder o comprimento de **varchar**, ele será mapeado para **LONGVARCHAR**. Da mesma forma, **nvarchar** mapeia para **LONGNVARCHAR** se o valor excede o comprimento com suporte de **nvarchar**. O mesmo é válido para **byte[]** . Valores maiores que **varbinary** se tornam **LONGVARBINARY**.

Há três categorias de conversões que têm suporte pelos métodos setObject do driver JDBC:

- **Sem perda (x)** : conversões para casos numéricos em que o tipo setter é o mesmo ou menor do que o tipo de servidor subjacente. Por exemplo, ao chamar setBigDecimal em uma coluna **decimal** do servidor subjacente, nenhuma conversão é necessária. Para casos de numérico para caractere, o tipo de dados Java **numeric** é convertido para uma **String**. Por exemplo, chamar setDouble com um valor de "53" em uma coluna de varchar (50) gerará um valor de caractere "53" na coluna de destino.

- **Convertido (y)** : conversões de um tipo **numérico** de Java para um tipo **numérico** de servidor subjacente menor. Esta conversão é normal e segue as convenções de conversão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A precisão sempre é truncada, nunca arredondada, e o estouro lança um erro de conversão sem suporte. Por exemplo, usar updateDecimal com um valor de "1.9999" em uma coluna de inteiro subjacente resulta em um "1" na coluna de destino; mas se for passado "3000000000", o driver lançará um erro.

- **Dependente de dados (z)** : conversões de um tipo **de cadeia de caracteres** Java [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o tipo de dados subjacente depende das seguintes condições: o driver envia o valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da **cadeia de caracteres** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executa conversões, se necessário. Se a propriedade de conexão sendStringParametersAsUnicode for definida como true e o tipo de dados subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for **imagem**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permitirá converter **nvarchar** em **imagem** e gerará um SQLServerException. Se sendStringParametersAsUnicode for definido como false e o tipo de dados subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for  **a imagem**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permitirá a conversão de **varchar** em **imagem** e não gerará uma exceção.

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza o conjunto de conversões em massa e passa os erros de volta para o driver JDBC quando há problemas. As conversões do lado do cliente são a exceção e são executadas somente no caso de **data**, **hora**, **timestamp**, **booliano**e  **Valores** de cadeia de caracteres.

Quando o tipo de dados da coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for **XML**, o valor de dados deverá ser um **XML** válido. Ao chamar os métodos setObject (byte [], SQLXML), setObject (inputStream, SQLXML) ou setObject (Blob, SQLXML), o valor de dados deverá ser a representação hexadecimal da cadeia dos caracteres XML. Por exemplo:

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Observe que uma marca de ordem de byte (BOM) é exigida se os caracteres XML estiverem em codificações de caracteres específicas.

## <a name="see-also"></a>Consulte Também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
