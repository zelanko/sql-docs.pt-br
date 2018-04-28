---
title: Programando com SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 91d2b0b1048b6385bcae2b3c9aa523962a4c1d22
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="programming-with-sqlxml"></a>Programando com SQLXML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esta seção descreve como usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos da API para armazenar e recuperar um XML de documento em e de um banco de dados relacional com **SQLXML** objetos.  
  
 Além disso, ela contém informações sobre os tipos de objetos SQLXML e fornece uma lista de diretrizes e limitações importantes referentes ao uso desses objetos.  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>Lendo e escrevendo dados XML com objetos SQLXML  
 A lista a seguir descreve como usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos da API para ler e gravar dados XML com objetos SQLXML:  
  
-   Para criar um objeto SQLXML, use o [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe. Observe que esse método cria um objeto SQLXML sem quaisquer dados. Para adicionar **xml** dados ao objeto SQLXML, chame um dos métodos a seguir que são especificados na interface SQLXML: setResult, setCharacterStream, setBinaryStream, ou setString.  
  
-   Para recuperar o objeto SQLXML propriamente dito, use os métodos getSQLXML do [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe ou o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe.  
  
-   Para recuperar o **xml** dados de um objeto SQLXML, use um dos seguintes métodos que são especificados na interface SQLXML: getSource, getCharacterStream, getBinaryStream, ou getString.  
  
-   Para atualizar o **xml** dados em um objeto SQLXML, use o [updateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe.  
  
-   Para armazenar um objeto SQLXML em uma coluna de tabela de banco de dados do tipo **xml**, use os métodos setSQLXML o [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe ou o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)classe.  
  
 O código de exemplo [exemplo de tipo de dados do SQLXML](../../connect/jdbc/sqlxml-data-type-sample.md) demonstra como executar essas tarefas comuns da API.  
  
## <a name="readable-and-writable-sqlxml-objects"></a>Objetos SQLXML que podem ser lidos e escritos  
 A tabela a seguir relaciona os tipos de objetos SQLXML que têm suporte dos métodos de setter, getter e updater fornecidos pela API do JDBC. As colunas da tabela referem-se ao seguinte:  
  
-   O **nome do método** coluna lista os métodos de getter, setter e updater com suporte na API do JDBC.  
  
-   O **objeto SQLXML de Getter** coluna representa um objeto SQLXML, que é criado pelo [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md) método o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe ou o [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe.  
  
-   O **objeto SQLXML de Setter** coluna representa um objeto SQLXML, que é criado pelo [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe. Observe que os métodos de setter abaixo aceitam apenas um objeto SQLXML criado pelo [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) método.  
  
|Nome do método|Objeto SQLXML de getter<br /><br /> (pode ser lido)|Objeto SQLXML de setter<br /><br /> (gravável)|  
|-----------------|-------------------------------------------|-------------------------------------------|  
|CallableStatement.setSQLXML()|Sem suporte|Tem suporte|  
|CallableStatement.setObject()|Sem suporte|Tem suporte|  
|PreparedStatement.setSQLXML()|Sem suporte|Tem suporte|  
|SetObject|Sem suporte|Tem suporte|  
|ResultSet.updateSQLXML()|Sem suporte|Tem suporte|  
|ResultSet.updateObject()|Sem suporte|Tem suporte|  
|ResultSet.getSQLXML()|Tem suporte|Sem suporte|  
|CallableStatement.getSQLXML()|Tem suporte|Sem suporte|  
  
 Como mostrado na tabela acima, os métodos SQLXML de setter não funcionarão com os objetos SQLXML que podem ser lidos; da mesma forma, os métodos de getter não funcionarão com os objetos SQLXML que podem ser escritos.  
  
 Se o aplicativo chama o método setObject especificando uma escala ou um parâmetro de comprimento com um objeto SQLXML, o parâmetro de escala ou comprimento será ignorado.  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>Diretrizes e limitações ao usar objetos SQLXML  
 Os aplicativos podem usar objetos SQLXML para ler e escrever os dados XML de e para o banco de dados. A lista a seguir fornece informações sobre limitações específicas e orientação quanto ao uso de objetos SQLXML:  
  
-   Um objeto SQLXML só pode ser válido pela duração da transação em que foi criado.  
  
-   Um objeto SQLXML recebido de um método de getter só pode ser usado para ler dados.  
  
-   Um objeto SQLXML criado pelo objeto de conexão só pode ser usado para escrever dados.  
  
-   O aplicativo só pode invocar um único método de getter em um objeto SQLXML legível para ler dados. Depois que o método de getter for invocado, ocorrerá falha em todos os outros métodos de getter ou setter no mesmo objeto SQLXML.  
  
-   O aplicativo pode chamar apenas o método free no objeto SQLXML depois que ela é lida ou gravada. Porém, ainda será possível processar a origem ou o fluxo retornado, contanto que a coluna ou o parâmetro subjacente esteja ativo. Se a coluna ou o parâmetro subjacente ficar inativo, a origem ou o fluxo associado com o objeto SQLXML será fechado. Se a coluna ou o parâmetro subjacente não for mais válido, os dados subjacentes não estarão disponíveis para os getters Fluxo, SAX (API Simples para XML) e StAX (API de Fluxo para XML).  
  
-   O aplicativo só pode invocar um único método de setter em um objeto SQLXML que pode ser escrito. Depois que o método de setter for invocado, ocorrerá falha em todos os outros métodos de setter ou getter no mesmo objeto SQLXML.  
  
-   Para definir dados no objeto SQLXML, o aplicativo deve usar o método de setter apropriado e as funções no objeto retornado.  
  
-   Os métodos getSQLXML o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe e o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe retorna **nulo** dados se a coluna subjacente for **nulo**.  
  
-   Os objetos de setter poderão ser válidos através da conexão dentro da qual forem criados.  
  
-   Aplicativos não têm permissão para definir um **nulo** valor usando os métodos de setter fornecidos pela interface SQLXML. Os aplicativos podem definir uma cadeia de caracteres vazia ("") usando os métodos de setter fornecidos na interface SQLXML. Para definir um **nulo** valor, os aplicativos devem chamar um dos seguintes:  
  
    -   Os métodos setNull o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe e [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe.  
  
    -   Os métodos setObject do [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe e [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe.  
  
    -   Os métodos setSQLXML o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe e [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe com um **nulo** o valor do parâmetro.  
  
-   Ao trabalhar com documentos XML, recomenda-se usar os analisadores SAX (API Simples para XML) e StAX (API de Fluxo para XML) em vez dos analisadores DOM (Document Object Model), por razões de desempenho.  
  
 Os analisadores de XML não podem tratar valores vazios. Porém, o SQL Server permite que os aplicativos recuperem e armazenem valores vazios de e para colunas de banco de dados do tipo de dados XML. Isso significa que, ao analisar os dados XML, se o valor subjacente for vazio, uma exceção será lançada pelo analisador. Para saídas de DOM, o driver JDBC captura essa exceção e lança um erro. Para saídas de SAX e StAX, o erro vem diretamente do analisador.  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>Buffer adaptável e suporte a SQLXML  
 Os fluxos binário e de caracteres retornados pelo objeto SQLXML obedecem aos modos de buffer adaptável ou completo. Por outro lado, se os analisadores de XML não forem fluxos, eles não obedecerão às configurações de adaptável ou completo. Para obter mais informações sobre buffer adaptável, consulte [buffer adaptável usando](../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dando suporte a dados XML](../../connect/jdbc/supporting-xml-data.md)  
  
  
