---
title: Usando tipos de dados avançados | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
caps.latest.revision: 58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ef615f695209cf01c2307c53effc7e84b06eb11
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278607"
---
# <a name="using-advanced-data-types"></a>Usando tipos de dados avançados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa os tipos de dados avançados do JDBC para converter os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] em um formato que possa ser compreendido pela linguagem de programação Java.  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir lista os mapeamentos padrão entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] avançado, o JDBC e os tipos de dados da linguagem de programação Java.  
  
|Tipos de SQL Server|Tipos JDBC (java.sql.Types)|Tipos da linguagem Java|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|byte[] \(default), Blob, InputStream, String|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String (default), Clob, InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (default), Clob, NClob (Java SE 6.0)|  
|xml|LONGVARCHAR<br /><br /> SQLXML (Java SE 6.0)|String (default), InputStream, Clob, byte[], Blob, SQLXML (Java SE 6.0)|  
|Udt<sup>1</sup>|VARBINARY|String (default), byte[], InputStream|  
  
 <sup>1</sup> O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte ao envio e à recuperação de UDTs CLR como dados binários, mas não à manipulação dos metadados CLR.  
  
 As seguintes seções fornecem exemplos de como é possível usar o driver JDBC e os tipos de dados avançados.  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>Tipos de dados BLOB e CLOB e NCLOB  
 O JDBC Driver implementa todos os métodos das interfaces java.sql.Blob, java.sql.Clob e java.sql.NClob.  
  
> [!NOTE]  
>  Os valores CLOB podem ser usados com tipos de dados de valor grande do [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] (ou posterior). Especificamente, tipos CLOB podem ser usados com o **varchar (max)** e **nvarchar (max)** tipos de dados, tipos BLOB podem ser usada com **varbinary (max)** e **imagem**  tipos de dados e tipos NCLOB podem ser usados com **ntext** e **nvarchar (max)**.  
  
## <a name="large-value-data-types"></a>Tipos de dados de valor grande  
 Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o trabalho com tipos de dados de valor grande exigia procedimentos especiais. Tipos de dados de valor grande são aqueles que excedem o tamanho de linha máximo de 8 KB. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] introduziu um especificador max para os tipos de dados **varchar**, **nvarchar** e **varbinary** a fim de permitir o armazenamento de valores de até 2^31 bytes. As colunas de tabela e as variáveis do [!INCLUDE[tsql](../../includes/tsql_md.md)] podem especificar os tipos de dados **varchar(max)**, **nvarchar(max)** ou **varbinary(max)**.  
  
 Os cenários primários para trabalhar com tipos de valor grande envolvem recuperá-los de um banco de dados ou adicioná-los a um banco de dados. As seções a seguir descrevem abordagens diferentes para realizar estas tarefas.  
  
### <a name="retrieving-large-value-types-from-a-database"></a>Recuperando tipos de valor grande de um banco de dados  
 Quando você recupera um tipo de dados de valor grande não binário – como o tipo de dados **varchar(max)** – de um banco de dados, uma abordagem é ler esses dados como um fluxo de caracteres. No exemplo a seguir, o método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) é usado para recuperar dados do banco de dados e retorná-los como um conjunto de resultados. Em seguida, o método [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) é usado para ler os dados de valor grande do conjunto de resultados.  
  
```java
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```  
  
> [!NOTE]  
>  Essa mesma abordagem também pode ser usada para o **texto**, **ntext**, e **nvarchar (max)** tipos de dados.  
  
 Quando você recupera um tipo de dados de valor grande e binário – como o tipo de dados **varbinary(max)** – de um banco de dados, existem diversas abordagens que você pode adotar. A abordagem mais eficiente é ler os dados como um fluxo binário, da seguinte maneira:  
  
```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```  
  
 Você também pode usar o método [getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) para ler os dados como uma matriz de bytes, da seguinte maneira:  
  
```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```  
  
> [!NOTE]  
>  Você também pode ler os dados como um BLOB. Porém, isto é menos eficiente que os dois métodos mostrados previamente.  
  
### <a name="adding-large-value-types-to-a-database"></a>Adicionando tipos de valor grande a um banco de dados  
 Carregar dados grandes com o driver JDBC funciona bem para os casos dimensionados por memória; nos casos maiores que a memória, streaming é a opção primária. Porém, o modo mais eficiente de carregar dados grandes é pelas interfaces de fluxo.  
  
 Usar uma cadeia de caracteres ou bytes também é uma opção, da seguinte maneira:  
  
```java
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```  
  
> [!NOTE]  
>  Essa abordagem também pode ser usada para valores que são armazenados em **texto**, **ntext**, e **nvarchar (max)** colunas.  
  
 Se você tiver uma biblioteca de imagem no servidor e precisar carregar arquivos de imagem binários inteiros para uma coluna **varbinary(max)**, o método mais eficiente com o driver JDBC será usar fluxos diretamente, da seguinte maneira:  
  
```java
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
 Na maioria dos casos, o método recomendado para atualizar ou modificar valores grandes no banco de dados é passar parâmetros pelas classes [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) usando comandos [!INCLUDE[tsql](../../includes/tsql_md.md)] como UPDATE, WRITE e SUBSTRING.  
  
 Se você precisar substituir a instância de uma palavra em um arquivo de texto grande, como um arquivo HTML arquivado, use um objeto Clob, da seguinte maneira:  
  
```java
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
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] fornece um tipo de dados **xml** que permite armazenar fragmentos e documentos XML em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. O tipo de dados **xml** é interno no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e tem algumas semelhanças com outros tipos internos, como **int** e **varchar**. Assim como ocorre com outros tipos internos, você pode usar o tipo de dados **xml** como um tipo de coluna ao criar uma tabela; como um tipo de variável, de parâmetro ou de retorno de função; ou em funções CAST e CONVERT do [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
 No driver JDBC, o tipo de dados **xml** pode ser mapeado como um objeto de Cadeia de Caracteres, matriz de bytes, fluxo, CLOB, BLOB ou SQLXML. Cadeia de caracteres é o padrão. A partir do JDBC Driver versão 2.0, o driver JDBC dá suporte à API do JDBC 4.0, que apresenta a interface SQLXML. A interface SQLXML define métodos para interagir com os dados XML e manipulá-los. O **SQLXML** tipo de dados é mapeado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** tipo de dados. Para obter mais informações sobre como ler e escrever dados XML bidirecionalmente no banco de dados relacional com o tipo de dados Java **SQLXML**, confira [Dando suporte a dados XML](../../connect/jdbc/supporting-xml-data.md).  
  
 A implementação do tipo de dados **xml** no driver JDBC fornece suporte para o seguinte:  
  
-   Acesso ao XML como uma cadeia de caracteres Java UTF-16 padrão para a maioria dos cenários comuns de programação  
  
-   Entrada de UTF-8 e outros XML codificados de 8 bits  
  
-   Acesso ao XML como uma matriz de byte com um BOM principal quando for codificado em UTF-16 para intercâmbio com outros processadores de XML e arquivos em disco  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] exige um BOM principal para XML codificado como UTF-16. O aplicativo deve fornecer isso quando os valores de parâmetro XML são fornecidos como matrizes de bytes. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sempre gera valores de saída XML como cadeias UTF-16 sem nenhum BOM nem uma declaração de codificação incorporada. Quando os valores XML são recuperados como byte[], BinaryStream ou Blob, um BOM UTF-16 é pré-demarcado no valor.  
  
 Para obter mais informações sobre os tipos de dados **xml**, confira "Tipo de dados xml" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="user-defined-data-type"></a>Tipo de dados definido pelo usuário  
 A introdução de UDTs (tipos definidos pelo usuário) no [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] estende o sistema de tipos SQL, permitindo que você armazene objetos e estruturas de dados personalizadas em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Os UDTs podem conter vários tipos de dados e ter comportamentos, o que os diferencia dos tipos de dados de alias tradicionais, que consistem em um único tipo de dado do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. As UDTs são definidas por usarem qualquer uma das linguagens para as quais o CLR do Microsoft .NET Framework oferece suporte e que produzem código verificável. Isto inclui Microsoft Visual C# e Visual Basic .NET. Os dados são expostos como campos e propriedades de uma classe ou estrutura baseada no .NET Framework, e os comportamentos são definidos pelos métodos da classe ou estrutura.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], um UDT pode ser usado como a definição da coluna de uma tabela, como uma variável em um lote do [!INCLUDE[tsql](../../includes/tsql_md.md)] ou como um argumento de uma função ou procedimento armazenado do [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
 Para obter mais informações sobre tipos de dados definidos pelo usuário, confira "Usando e modificando instâncias de tipos definidos pelo usuário" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
