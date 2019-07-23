---
title: Exemplo de tipo de dados SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8f2ff25b-71fd-46d7-b6de-d656095d2aad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d5e616fa1a510633caf4e5e2e0b20266a1eb771
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004379"
---
# <a name="sqlxml-data-type-sample"></a>Exemplo de tipo de dados SQLXML

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstra como armazenar dados XML em um banco de dados relacional, como recuperar dados XML de um banco de dados e como analisar dados XML com o tipo de dados Java **SQLXML**.

Os exemplos de código nesta seção usam um analisador SAX (API Simples para XML). O SAX é um padrão publicamente desenvolvido para a análise de documentos XML baseada em eventos. Ele também fornece uma interface de programação de aplicativos para trabalhar com dados XML. Observe que os aplicativos também podem usar qualquer outro analisador de XML, como, por exemplo, o Modelo de Objeto de Documento (DOM) ou a StAX (API de Fluxo para XML), ou assim por diante.

O Modelo de Objeto de Documento (DOM) fornece uma representação programática de documentos XML, fragmentos, nós ou conjuntos de nó. Ele também fornece uma interface de programação de aplicativos para trabalhar com dados XML. Da mesma forma, a StAX (API de Fluxo para XML) é uma API baseada em Java para análise de recepção de XML.

> [!IMPORTANT]  
> Para usar a API do analisador de SAX, você deve importar a implementação de SAX padrão do pacote javax.xml.

O arquivo de código desta amostra chama-se SqlXmlDataType.java e pode ser encontrado no seguinte local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo sqljdbc4.jar. Se uma entrada para sqljdbc4.jar estiver ausente no classpath, o aplicativo de exemplo gerará a exceção "Classe não encontrada". Para obter mais informações sobre como definir o classpath, consulte [usando o driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

Além disso, você precisa ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] para executar este aplicativo de exemplo.

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] e, em seguida, chama o método createSampleTables.

O método createSampleTables removerá as tabelas de teste, TestTable1 e TestTable2, caso elas existam. Então, ele insere duas linhas em TestTable1.

Além disso, o exemplo de código inclui os três métodos a seguir e uma classe adicional que é denominada ExampleContentHandler.

A classe ExampleContentHandler implementa um manipulador de conteúdo personalizado, que define métodos para eventos de analisador.

O método showGetters demonstra como analisar os dados no objeto SQLXML usando o SAX, ContentHandler e XMLReader. Primeiro, o exemplo de código cria uma instância de um manipulador de conteúdo personalizado, que é ExampleContentHandler. Em seguida, ele cria e executa uma instrução SQL que retorna um conjunto de dados de TestTable1. Então, o exemplo de código obtém um analisador de SAX e analisa os dados XML.

O método showSetters demonstra como definir a coluna **xml** usando o SAX, ContentHandler e ResultSet. Primeiro, ele cria um objeto SQLXML vazio usando o método [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) da classe Connection. Então, ele obtém uma instância de um manipulador de conteúdo para gravar os dados no objeto SQLXML. Em seguida, o exemplo de código grava os dados em TestTable1. Por fim, o código de exemplo itera pelas linhas de dados do conjunto de resultados e usa o método [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) para ler os dados XML.

O método showTransformer demonstra como obter dados XML de uma tabela e inserir esses dados XML em outra tabela usando SAX e Transformer. Primeiro, ele recupera o objeto SQLXML de origem do TestTable1. Em seguida, ele cria um objeto SQLXML de destino vazio usando o método [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) da classe Connection. Em seguida, ele atualiza o objeto SQLXML de destino e grava os dados XML em TestTable2. Por fim, o código de exemplo itera pelas linhas de dados do conjunto de resultados e usa o método [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) para ler os dados XML em TestTable2.

[!code[JDBC#UsingSQLXML1](../../connect/jdbc/codesnippet/Java/sqlxml-data-type-sample_1.java)]

## <a name="see-also"></a>Consulte Também

[Trabalhando com tipos de dados &#40;JDBC&#41;](../../connect/jdbc/working-with-data-types-jdbc.md)
