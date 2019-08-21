---
title: Lendo exemplo de dados grandes | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 260666488a21b02c0c318d3277b72fc576b0ab08
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027817"
---
# <a name="reading-large-data-sample"></a>Lendo exemplo de dados grandes

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstra como recuperar um valor grande de coluna única de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o método [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md).

O arquivo de código desta amostra chama-se ReadLargeData.java e pode ser encontrado no seguinte local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, você precisará ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Você também precisará definir o classpath para incluir o arquivo mssql-jdbc.jar. Para obter mais informações sobre como definir o classpath, consulte [usando o driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para saber mais sobre qual arquivo JAR escolher, confira os [requisitos do sistema para o JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Em seguida, o código de exemplo cria dados de exemplo e atualiza a tabela Production.Document usando uma consulta parametrizada.

Além disso, o código de exemplo demonstra como obter o modo de buffer adaptável usando o método [getResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Observe que, a partir da versão 2.0 do driver JDBC, a propriedade de conexão responseBuffering é definida por padrão como "adaptável".

Em seguida, usando uma instrução SQL com o objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), o código de exemplo executa a instrução SQL e coloca os dados retornados em um objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).

Por fim, o código de exemplo itera pelas linhas de dados do conjunto de resultados e usa o método [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) para acessar alguns dos dados.

[!code[JDBC#UsingAdaptiveBuffering1](../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]

## <a name="see-also"></a>Confira também

[Trabalhando com dados grandes](../../connect/jdbc/working-with-large-data.md)
