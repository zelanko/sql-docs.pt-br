---
title: Programando com SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8d88f6c9febf582aa9aca3d47931ceb72074c87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956171"
---
# <a name="programming-with-sqlxml"></a>Programando com SQLXML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esta seção descreve como usar os métodos da API [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para armazenar e recuperar um documento XML em um banco de dados relacional, ou vindo dele, com objetos **SQLXML**.  
  
 Além disso, ela contém informações sobre os tipos de objetos SQLXML e fornece uma lista de diretrizes e limitações importantes referentes ao uso desses objetos.  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>Lendo e escrevendo dados XML com objetos SQLXML  
 A lista a seguir descreve como usar os métodos da API [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para ler e gravar dados XML com objetos SQLXML:  
  
-   Para criar um objeto SQLXML, use o método [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Observe que esse método cria um objeto SQLXML sem quaisquer dados. Para adicionar dados **XML** ao objeto SQLXML, chame um dos seguintes métodos especificados na interface do SQLXML: setResult, SetCharacterStream, setBinaryStream ou SetString.  
  
-   Para recuperar o objeto SQLXML propriamente dito, use os métodos getSQLXML da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) ou da classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
-   Para recuperar os dados **XML** de um objeto SQLXML, use um dos seguintes métodos especificados na interface do SQLXML: GetSource, GetCharacterStream, getBinaryStream ou GetString.  
  
-   Para atualizar os dados **xml** em um objeto SQLXML, use o método [updateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
-   Para armazenar um objeto SQLXML em uma coluna de tabela de banco de dados do tipo **xml**, use os métodos setSQLXML da classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) ou da classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
 O código de exemplo em [Exemplo de tipo de dados SQLXML](../../connect/jdbc/sqlxml-data-type-sample.md) demonstra como executar essas tarefas de API comuns.  
  
## <a name="readable-and-writable-sqlxml-objects"></a>Objetos SQLXML que podem ser lidos e escritos  
 A tabela a seguir relaciona os tipos de objetos SQLXML que têm suporte dos métodos de setter, getter e updater fornecidos pela API do JDBC. As colunas da tabela referem-se ao seguinte:  
  
-   A coluna **Nome do método** lista os métodos de getter, setter e updater compatíveis com a API do JDBC.  
  
-   A coluna **Objeto SQLXML de getter** representa um objeto SQLXML que é criado pelo método [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md) da classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) ou pelo método [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
-   A coluna **Objeto SQLXML de setter** representa um objeto SQLXML que é criado pelo método [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Observe que os métodos de setter indicados abaixo só aceitam um objeto SQLXML criado pelo método [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md).  
  
|Nome do método|Objeto SQLXML de getter<br /><br /> (pode ser lido)|Objeto SQLXML de setter<br /><br /> (gravável)|  
|-----------------|-------------------------------------------|-------------------------------------------|  
|CallableStatement.setSQLXML()|Sem suporte|Tem suporte|  
|CallableStatement.setObject()|Sem suporte|Tem suporte|  
|PreparedStatement.setSQLXML()|Sem suporte|Tem suporte|  
|PreparedStatement.setObject()|Sem suporte|Tem suporte|  
|ResultSet.updateSQLXML()|Sem suporte|Tem suporte|  
|ResultSet.updateObject()|Sem suporte|Tem suporte|  
|ResultSet.getSQLXML()|Tem suporte|Sem suporte|  
|CallableStatement.getSQLXML()|Tem suporte|Sem suporte|  
  
 Como mostrado na tabela acima, os métodos SQLXML de setter não funcionarão com os objetos SQLXML que podem ser lidos; da mesma forma, os métodos de getter não funcionarão com os objetos SQLXML que podem ser escritos.  
  
 Se o aplicativo invocar o método setObject especificando uma escala ou um parâmetro de tamanho com um objeto SQLXML, o parâmetro de escala ou tamanho será ignorado.  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>Diretrizes e limitações ao usar objetos SQLXML  
 Os aplicativos podem usar objetos SQLXML para ler e escrever os dados XML de e para o banco de dados. A lista a seguir fornece informações sobre limitações específicas e orientação quanto ao uso de objetos SQLXML:  
  
-   Um objeto SQLXML só pode ser válido pela duração da transação em que foi criado.  
  
-   Um objeto SQLXML recebido de um método de getter só pode ser usado para ler dados.  
  
-   Um objeto SQLXML criado pelo objeto de conexão só pode ser usado para escrever dados.  
  
-   O aplicativo só pode invocar um único método de getter em um objeto SQLXML legível para ler dados. Depois que o método de getter for invocado, ocorrerá falha em todos os outros métodos de getter ou setter no mesmo objeto SQLXML.  
  
-   O aplicativo só pode invocar o método gratuito no objeto SQLXML depois que ele é lido ou gravado. Porém, ainda será possível processar a origem ou o fluxo retornado, contanto que a coluna ou o parâmetro subjacente esteja ativo. Se a coluna ou o parâmetro subjacente ficar inativo, a origem ou o fluxo associado com o objeto SQLXML será fechado. Se a coluna ou o parâmetro subjacente não for mais válido, os dados subjacentes não estarão disponíveis para os getters Fluxo, SAX (API Simples para XML) e StAX (API de Fluxo para XML).  
  
-   O aplicativo só pode invocar um único método de setter em um objeto SQLXML que pode ser escrito. Depois que o método de setter for invocado, ocorrerá falha em todos os outros métodos de setter ou getter no mesmo objeto SQLXML.  
  
-   Para definir dados no objeto SQLXML, o aplicativo deve usar o método de setter apropriado e as funções no objeto retornado.  
  
-   Os métodos getSQLXML da classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) e da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) retornarão dados **null** se a coluna subjacente for **null**.  
  
-   Os objetos de setter poderão ser válidos através da conexão dentro da qual forem criados.  
  
-   Os aplicativos não têm permissão para definir um valor **null** usando os métodos de setter fornecidos pela interface SQLXML. Os aplicativos podem definir uma cadeia de caracteres vazia ("") usando os métodos de setter fornecidos na interface SQLXML. Para definir um valor **null**, os aplicativos precisam chamar um dos seguintes itens:  
  
    -   Os métodos setNull das classes [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) e [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
    -   Os métodos setObject das classes [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) e [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
    -   Os métodos setSQLXML das classes [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) e [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) com um valor de parâmetro **null**.  
  
-   Ao trabalhar com documentos XML, recomenda-se usar os analisadores SAX (API Simples para XML) e StAX (API de Fluxo para XML) em vez dos analisadores DOM (Document Object Model), por razões de desempenho.  
  
 Os analisadores de XML não podem tratar valores vazios. Porém, o SQL Server permite que os aplicativos recuperem e armazenem valores vazios de e para colunas de banco de dados do tipo de dados XML. Isso significa que, ao analisar os dados XML, se o valor subjacente for vazio, uma exceção será lançada pelo analisador. Para saídas de DOM, o driver JDBC captura essa exceção e lança um erro. Para saídas de SAX e StAX, o erro vem diretamente do analisador.  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>Buffer adaptável e suporte a SQLXML  
 Os fluxos binário e de caracteres retornados pelo objeto SQLXML obedecem aos modos de buffer adaptável ou completo. Por outro lado, se os analisadores de XML não forem fluxos, eles não obedecerão às configurações de adaptável ou completo. Para obter mais informações sobre o buffer adaptável, consulte [usando o buffer adaptável](../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Dando suporte a dados XML](../../connect/jdbc/supporting-xml-data.md)  
  
  
