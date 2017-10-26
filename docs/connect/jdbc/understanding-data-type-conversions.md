---
title: "Conversões de tipo de dados de Conhecimento | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b8a4439d9682435baca0867dfc9d8bd96d0fcd7c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-data-type-conversions"></a>Entendendo conversões de tipo de dados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para facilitar a conversão de tipos de dados de linguagem de programação Java [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece conversões de tipo de dados conforme exigido pela especificação do JDBC. Para garantir flexibilidade, todos os tipos são conversíveis para e de **objeto**, **cadeia de caracteres**, e **byte []** tipos de dados.  
  
## <a name="getter-method-conversions"></a>Conversões de método getter  
 Com base no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados, o gráfico a seguir contém o mapa de conversão do driver JDBC para get\<tipo > métodos () a [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe e as conversões com suporte para get\< Tipo > métodos do [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe.  
  
 ![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")  
  
 Há três categorias de conversões que têm suporte pelos métodos getter do driver JDBC:  
  
-   **Sem perda (x)**: conversões para casos em que o tipo getter é o mesmo ou menor do que o tipo de servidor subjacente. Por exemplo, ao chamar getBigDecimal em uma coluna decimal do servidor subjacente, nenhuma conversão é necessária.  
  
-   **Convertido (y)**: conversões de tipos de servidores numéricos para tipos de linguagem Java em que a conversão é normal e segue as regras de conversão de linguagem Java. Para estas conversões, a precisão é sempre truncada — nunca arredondada — e o estouro é tratado como módulo do tipo de destino, que é menor. Por exemplo, chamar getInt em uma base **decimal** coluna que contém "1.9999" retornará "1", ou se subjacente **decimal** valor for "3000000000", o **int** valor estourará para "-1294967296".  
  
-   **Dependente de dados (z)**: conversões de tipos de caracteres subjacentes para tipos numéricos exigem que os tipos de caracteres contenham valores que podem ser convertidos naquele tipo. Nenhuma outra conversão é realizada. Se o valor for muito grande para o tipo getter, o valor não será válido. Por exemplo, se getInt for chamado em uma coluna de varchar (50) que contém "53", o valor é retornado como um **int**; mas se o valor subjacente for "xyz" ou "3000000000", um erro será lançado.  
  
 Se getString for chamado em um **binário**, **varbinary**, **varbinary (max)**, ou **imagem** tipo de dados de coluna, o valor é retornado como um valor de cadeia de caracteres hexadecimal.  
  
## <a name="updater-method-conversions"></a>Conversões de método updater  
 Para os tipo Java passados para a atualização de dados\<tipo > métodos () a [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe, as seguintes conversões se aplicam.  
  
 ![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")  
  
 Há três categorias de conversões que têm suporte pelos métodos updater do driver JDBC:  
  
-   **Sem perda (x)**: conversões para casos em que o tipo updater é o mesmo ou menor do que o tipo de servidor subjacente. Por exemplo, ao chamar updateBigDecimal em uma coluna decimal do servidor subjacente, nenhuma conversão é necessária.  
  
-   **Convertido (y)**: conversões de tipos de servidores numéricos para tipos de linguagem Java em que a conversão é normal e segue as regras de conversão de linguagem Java. Para estas conversões, a precisão é sempre truncada (nunca arredondada) e o estouro é tratado como módulo do tipo de destino (menor). Por exemplo, chamar updateDecimal em uma base **int** coluna que contém "1.9999" retornará "1", ou se subjacente **decimal** valor for "3000000000", o **int**valor estourará para "-1294967296".  
  
-   **Dependente de dados (z)**: conversões de tipos de dados de origem subjacentes para tipos de dados de destino exigem que os valores contidos podem ser convertidos em tipos de destino. Nenhuma outra conversão é realizada. Se o valor for muito grande para o tipo getter, o valor não será válido. Por exemplo, se updateString for chamado em uma coluna int que contém "53", a atualização será bem-sucedida; mas se o valor subjacente de String for "foo" ou "3000000000", um erro será lançado.  
  
 Quando updateString for chamado em um **binário**, **varbinary**, **varbinary (max)**, ou **imagem** tipo de dados de coluna, ele trata o valor de cadeia de caracteres como um valor de cadeia de caracteres hexadecimal.  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é do tipo de dados de coluna **XML**, o valor de dados deve ser um válido **XML**. Ao chamar métodos updateBlob, updateBinaryStream ou updateBytes, o valor de dados deve ser a representação de cadeia de caracteres hexadecimal dos caracteres XML. Por exemplo:  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 Observe que uma marca de ordem de byte (BOM) é exigida se os caracteres XML estiverem em codificações de caracteres específicas.  
  
## <a name="setter-method-conversions"></a>Conversões de método setter  
 Para os tipo Java passados para o conjunto de dados\<tipo > métodos () a [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe e o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe, as seguintes conversões se aplicam.  
  
 ![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")  
  
 O servidor experimenta qualquer conversão e retorna erros quando há falha.  
  
 No caso do **cadeia de caracteres** tipo de dados, se o valor excede o comprimento de **VARCHAR**, ele é mapeado para **LONGVARCHAR**. Da mesma forma, **NVARCHAR** mapeia para **LONGNVARCHAR** se o valor excede o tamanho com suporte de **NVARCHAR**. O mesmo é verdadeiro para **byte []**. Valores maiores que **VARBINARY** se tornar **LONGVARBINARY**.  
  
 Há duas categorias de conversões que têm suporte pelos métodos setter do driver JDBC:  
  
-   **Sem perda (x)**: conversões para casos numéricos em que o tipo setter é o mesmo ou menor do que o tipo de servidor subjacente. Por exemplo, ao chamar setBigDecimal em um servidor subjacente **decimal** coluna, nenhuma conversão é necessária. Para casos de caractere, o Java de numérico para **numérico** tipo de dados é convertido em um **cadeia de caracteres**. Por exemplo, chamar setDouble com um valor de "53" em uma coluna de varchar (50) gera um valor de caractere "53" na coluna de destino.  
  
-   **Convertido (y)**: conversões de um Java **numérico** tipo para um servidor subjacente **numérico** tipo menor. Essa conversão é normal e segue [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] convenções de conversão. A precisão sempre é truncada (nunca arredondada) e o estouro lança um erro de conversão sem suporte. Por exemplo, usando updateDecimal com um valor de "1.9999" em uma base resultados de coluna de inteiro em um "1" na coluna de destino; mas se for passado "3000000000", o driver gerará um erro.  
  
-   **Dependente de dados (z)**: conversões de um Java **cadeia de caracteres** tipo subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] depende do tipo de dados das seguintes condições: O driver envia o **cadeia de caracteres** valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] executa conversões, se necessário. Se sendStringParametersAsUnicode for definido como true e subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é do tipo de dados **imagem**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] não permitirá a conversão **nvarchar** para **deimagem** e lançará um SQLServerException. Se sendStringParametersAsUnicode for definido como false e subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é do tipo de dados **imagem**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permitirá a conversão de **varchar** para **imagem**e não gerará uma exceção.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]realiza as conversões e passa os erros de volta para o driver JDBC quando há problemas.  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é do tipo de dados de coluna **XML**, o valor de dados deve ser um válido **XML**. Ao chamar métodos updateBlob, updateBinaryStream ou updateBytes, o valor de dados deve ser a representação de cadeia de caracteres hexadecimal dos caracteres XML. Por exemplo:  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 Observe que uma marca de ordem de byte (BOM) é exigida se os caracteres XML estiverem em codificações de caracteres específicas.  
  
## <a name="conversions-on-setobject"></a>Conversões em setObject  
  
> [!NOTE]  
>  Microsoft JDBC Drivers 4.2 (e superior) para SQL Server oferece suporte a JDBC 4.1 e 4.2. Para obter mais detalhes sobre mapeamentos de tipo de dados e conversões de 4.1 e 4.2 consulte [conformidade JDBC 4.1 para o Driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e [conformidade do JDBC 4.2 para o Driver JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md), além das informações abaixo.  
  
 Para os tipo Java dados passados para a setObject (\<tipo >) métodos do [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe, as seguintes conversões se aplicam.  
  
 ![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")  
  
 O método setObject sem tipo designado especificado usa o mapeamento padrão. No caso do **cadeia de caracteres** tipo de dados, se o valor excede o comprimento de **VARCHAR**, ele é mapeado para **LONGVARCHAR**. Da mesma forma, **NVARCHAR** mapeia para **LONGNVARCHAR** se o valor excede o tamanho com suporte de **NVARCHAR**. O mesmo é verdadeiro para **byte []**. Valores maiores que **VARBINARY** se tornar **LONGVARBINARY**.  
  
 Há três categorias de conversões que têm suporte pelos métodos setObject do driver JDBC:  
  
-   **Sem perda (x)**: conversões para casos numéricos em que o tipo setter é o mesmo ou menor do que o tipo de servidor subjacente. Por exemplo, ao chamar setBigDecimal em um servidor subjacente **decimal** coluna, nenhuma conversão é necessária. Para casos de caractere, o Java de numérico para **numérico** tipo de dados é convertido em um **cadeia de caracteres**. Por exemplo, chamar setDouble com um valor de "53" em uma coluna de varchar (50) produzir um valor de caractere "53" na coluna de destino.  
  
-   **Convertido (y)**: conversões de um Java **numérico** tipo para um servidor subjacente **numérico** tipo menor. Essa conversão é normal e segue [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] convenções de conversão. A precisão sempre é truncada — nunca arredondada — e o estouro lança um erro de conversão sem suporte. Por exemplo, usando updateDecimal com um valor de "1.9999" em uma base resultados de coluna de inteiro em um "1" na coluna de destino; mas se for passado "3000000000", o driver gerará um erro.  
  
-   **Dependente de dados (z)**: conversões de um Java **cadeia de caracteres** tipo subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] depende do tipo de dados das seguintes condições: O driver envia o **cadeia de caracteres** valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] executa conversões, se necessário. Se a propriedade de conexão sendStringParametersAsUnicode for definida como true e subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é do tipo de dados **imagem**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] não permitirá a conversão **nvarchar** para **imagem** e lançará um SQLServerException. Se sendStringParametersAsUnicode for definido como false e subjacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é do tipo de dados **imagem**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permitirá a conversão de **varchar** para **imagem**e não gerará uma exceção.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]executa o conjunto de conversões em massa e passa os erros de volta para o driver JDBC quando há problemas. Conversões do lado do cliente são a exceção e são executadas somente no caso de **data**, **tempo**, **timestamp**, **booliano**e ** Cadeia de caracteres** valores.  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é do tipo de dados de coluna **XML**, o valor de dados deve ser um válido **XML**. Ao chamar os métodos setObject (byte [], SQLXML), setObject (inputStream, SQLXML) ou setObject (Blob, SQLXML), o valor de dados deverá ser a representação hexadecimal da cadeia dos caracteres XML. Por exemplo:  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 Observe que uma marca de ordem de byte (BOM) é exigida se os caracteres XML estiverem em codificações de caracteres específicas.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

