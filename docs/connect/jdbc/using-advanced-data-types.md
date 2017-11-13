---
title: "Usando tipos de dados avançados | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
caps.latest.revision: 58
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b74ed587d91e351f91db2e3ef2a45c41edf37918
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-advanced-data-types"></a>Usando tipos de dados avançados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa os tipos de dados avançados JDBC para converter o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados em um formato que possa ser compreendido pela Java linguagem de programação.  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir lista os mapeamentos padrão entre o avançado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], JDBC e os tipos de dados da linguagem de programação Java.  
  
|Tipos de SQL Server|Tipos JDBC (java.sql.Types)|Tipos da linguagem Java|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|Byte [] \(padrão), Blob, InputStream, cadeia de caracteres|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String (default), Clob, InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (default), Clob, NClob (Java SE 6.0)|  
|xml|LONGVARCHAR<br /><br /> SQLXML (Java SE 6.0)|String (default), InputStream, Clob, byte[],Blob, SQLXML (Java SE 6.0)|  
|UDT<sup>1</sup>|VARBINARY|String (default), byte[], InputStream|  
  
 <sup>1</sup> o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte ao envio e recuperação de UDTs CLR como dados binários, mas não à manipulação dos metadados CLR.  
  
 As seguintes seções fornecem exemplos de como é possível usar o driver JDBC e os tipos de dados avançados.  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>Tipos de dados BLOB e CLOB e NCLOB  
 O JDBC Driver implementa todos os métodos das interfaces java.sql.Blob, java.sql.Clob e java.sql.NClob.  
  
> [!NOTE]  
>  Os valores CLOB podem ser usados com [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] (ou posterior) tipos de dados de valor grande. Especificamente, tipos CLOB podem ser usados com o **varchar (max)** e **nvarchar (max)** tipos de dados, tipos BLOB podem ser usada com **varbinary (max)** e **imagem**  tipos de dados e tipos NCLOB podem ser usados com **ntext** e **nvarchar (max)**.  
  
## <a name="large-value-data-types"></a>Tipos de dados de valor grande  
 Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], trabalhar com tipos de dados de valor grande exigia procedimentos de especiais. Tipos de dados de valor grande são aqueles que excedem o tamanho de linha máximo de 8 KB. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]apresenta um especificador max para **varchar**, **nvarchar**, e **varbinary** tipos de dados para permitir o armazenamento de valores tão grandes quanto 2 ^ 31 bytes. Colunas da tabela e [!INCLUDE[tsql](../../includes/tsql_md.md)] podem especificar variáveis **varchar (max)**, **nvarchar (max)**, ou **varbinary (max)** tipos de dados.  
  
 Os cenários primários para trabalhar com tipos de valor grande envolvem recuperá-los de um banco de dados ou adicioná-los a um banco de dados. As seções a seguir descrevem abordagens diferentes para realizar estas tarefas.  
  
### <a name="retrieving-large-value-types-from-a-database"></a>Recuperando tipos de valor grande de um banco de dados  
 Quando você recuperar um tipo de dados de valor grande não binário — como o **varchar (max)** tipo de dados — de um banco de dados, uma abordagem é ler esses dados como um fluxo de caracteres. No exemplo a seguir, o [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe é usada para recuperar dados do banco de dados e retorná-lo como um conjunto de resultados. Em seguida, o [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe é usada para ler os dados de valor grande do conjunto de resultados.  
  
```  
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```  
  
> [!NOTE]  
>  Essa mesma abordagem também pode ser usada para o **texto**, **ntext**, e **nvarchar (max)** tipos de dados.  
  
 Quando você recuperar um tipo de dados de grande valor binário — como o **varbinary (max)** tipo de dados — de um banco de dados, há várias abordagens que podem ser executadas. A abordagem mais eficiente é ler os dados como um fluxo binário, da seguinte maneira:  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```  
  
 Você também pode usar o [getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) método para ler os dados como uma matriz de bytes, como no exemplo a seguir:  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```  
  
> [!NOTE]  
>  Você também pode ler os dados como um BLOB. Porém, isto é menos eficiente que os dois métodos mostrados previamente.  
  
### <a name="adding-large-value-types-to-a-database"></a>Adicionando tipos de valor grande a um banco de dados  
 Carregar dados grandes com o driver JDBC funciona bem para os casos dimensionados por memória; nos casos maiores que a memória, streaming é a opção primária. Porém, o modo mais eficiente de carregar dados grandes é pelas interfaces de fluxo.  
  
 Usar uma cadeia de caracteres ou bytes também é uma opção, da seguinte maneira:  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```  
  
> [!NOTE]  
>  Essa abordagem também pode ser usada para valores que são armazenados em **texto**, **ntext**, e **nvarchar (max)** colunas.  
  
 Se você tiver uma biblioteca de imagens no servidor e precisar carregar arquivos de imagem binários inteiros para uma **varbinary (max)** coluna, o método mais eficiente com o driver JDBC será usar fluxos diretamente, como no exemplo a seguir:  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)");  
File inputFile = new File("CLOBFile20mb.jpg");  
FileInputStream inStream = new FileInputStream(inputFile);  
int id = 1;  
pstmt.setInt(1,id);  
pstmt.setBinaryStream(2, inStream);  
pstmt.executeUpdate();  
inStream.close();  
```  
  
> [!NOTE]  
>  Usar o método CLOB ou BLOB não é uma maneira eficiente de carregar dados grandes.  
  
### <a name="modifying-large-value-types-in-a-database"></a>Modificando tipos de valor grande em um banco de dados  
 Na maioria dos casos, o método recomendado para atualizar ou modificar valores grandes no banco de dados é passar parâmetros por meio de [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classes usando [!INCLUDE[tsql](../../includes/tsql_md.md)] comandos como UPDATE, WRITE e SUBSTRING.  
  
 Se você tiver que substituir a instância de uma palavra em um arquivo de texto grande, como um arquivo HTML, você pode usar um objeto Clob, como a seguir:  
  
```  
String SQL = "SELECT * FROM test1;";  
Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
ResultSet rs = stmt.executeQuery(SQL);  
rs.next();  
  
Clob clob = rs.getClob(2);  
long pos = clob.position("dog", 1);  
clob.setString(pos, "cat");  
rs.updateClob(2, clob);  
rs.updateRow();  
```  
  
 Adicionalmente, você pode fazer todo o trabalho no servidor e só passar parâmetros para uma instrução UPDATE preparada.  
  
 Para obter mais informações sobre tipos de valor grande, consulte "Usando tipos de valor grande" nos Manuais Online do SQL Server.  
  
## <a name="xml-data-type"></a>Tipo de dados XML  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Fornece um **xml** tipo de dados que permite armazenar documentos XML e fragmentos em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. O **xml** tipo de dados é um tipo de dados internos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]e é em algumas semelhanças com outros tipos internos, como **int** e **varchar**. Como com outros tipos internos, você pode usar o **xml** tipo de dados como um tipo de coluna quando você cria uma tabela; como um tipo de variável, um tipo de parâmetro ou um tipo de retorno de função; ou em [!INCLUDE[tsql](../../includes/tsql_md.md)] funções CAST e CONVERT.  
  
 No driver JDBC, o **xml** tipo de dados pode ser mapeado como uma cadeia de caracteres, a matriz de bytes, o fluxo, o objeto CLOB, BLOB ou SQLXML. Cadeia de caracteres é o padrão. A partir do JDBC Driver versão 2.0, o driver JDBC dá suporte à API do JDBC 4.0, que apresenta a interface SQLXML. A interface SQLXML define métodos para interagir e manipular dados XML. O **SQLXML** tipo de dados mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** tipo de dados. Para obter mais informações sobre como ler e escrever dados XML de e para o banco de dados relacional com o **SQLXML** tipo de dados Java, consulte [dando suporte a dados de XML](../../connect/jdbc/supporting-xml-data.md).  
  
 A implementação de **xml** tipo de dados no JDBC driver fornece suporte para o seguinte:  
  
-   Acesso ao XML como uma cadeia de caracteres Java UTF-16 padrão para a maioria dos cenários comuns de programação  
  
-   Entrada de UTF-8 e outros XML codificados de 8 bits  
  
-   Acesso ao XML como uma matriz de byte com um BOM principal quando for codificado em UTF-16 para intercâmbio com outros processadores de XML e arquivos em disco  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]exige um BOM principal para XML codificado em UTF-16. O aplicativo deve fornecer isso quando os valores de parâmetro XML são fornecidos como matrizes de bytes. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]sempre produz valores XML como UTF-16 cadeias de caracteres com nenhuma BOM ou declaração de codificação incorporada. Quando os valores XML são recuperados como byte[], BinaryStream ou Blob, um BOM UTF-16 é pré-demarcado no valor.  
  
 Para obter mais informações sobre o **xml** tipo de dados, consulte "tipo de dados xml" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="user-defined-data-type"></a>Tipo de dados definido pelo usuário  
 A introdução de tipos definidos pelo usuário (UDTs) em [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] estende o sistema de tipo SQL, permitindo armazenar objetos e estruturas de dados personalizadas em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Os UDTs podem conter vários tipos de dados e ter comportamentos, o que os diferencia dos tipos de dados de alias tradicionais, que consistem em um único tipo de dado do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. As UDTs são definidas por usarem qualquer uma das linguagens para as quais o CLR do Microsoft .NET Framework oferece suporte e que produzem código verificável. Isto inclui Microsoft Visual C# e Visual Basic .NET. Os dados são expostos como campos e propriedades de uma classe ou estrutura baseada no .NET Framework, e os comportamentos são definidos pelos métodos da classe ou estrutura.  
  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], um UDT pode ser usado como a definição de coluna de uma tabela, como uma variável em uma [!INCLUDE[tsql](../../includes/tsql_md.md)] em lotes, ou como um argumento de uma [!INCLUDE[tsql](../../includes/tsql_md.md)] função ou procedimento armazenado.  
  
 Para obter mais informações sobre os tipos de dados definidos pelo usuário, consulte "Usando e modificando instâncias de tipos definidos pelo usuário" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

