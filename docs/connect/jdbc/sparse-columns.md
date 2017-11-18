---
title: Colunas esparsas | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7d4237e0-818f-4639-9093-d5ac9683fc71
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e70b83f9c419c6d619ce4e90697e40289f4d9ae4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sparse-columns"></a>Colunas esparsas
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Colunas esparsas são colunas comuns que têm um armazenamento otimizado para valores nulos. Elas reduzem os requisitos de espaço para valores nulos à custa de maior sobrecarga para recuperar valores não nulos. Considere o uso de colunas esparsas quando o espaço salvo for pelo menos de 20 a 40 por cento.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0 oferece suporte a colunas esparsas quando você se conectar a um [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] (ou posterior) server. Você pode usar [Getcolumns](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md), [sqlserverdatabasemetadata. Getfunctioncolumns](../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md), ou [sqlserverdatabasemetadata. Getprocedurecolumns](../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md) para determinar qual coluna é esparsa e qual coluna é a coluna de conjunto de coluna.  
  
 Conjuntos de coluna são colunas computadas que retornam todas as colunas esparsas na forma de XML sem tipo. Considere o uso de conjuntos de colunas quando o número de colunas em uma tabela for grande ou maior que 1024, ou quando trabalhar nessas colunas esparsas individualmente for difícil. Um conjunto de colunas pode conter até 30.000 colunas.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Description  
 Este exemplo demonstra como detectar conjuntos de colunas. Ele também mostra como analisar a saída XML de um conjunto de colunas para obter os dados das colunas esparsas.  
  
 O primeiro código que lista o Transact-SQL a ser executado no servidor.  
  
 O segundo código que lista o código-fonte Java. Antes de compilar o aplicativo, altere o nome do servidor na cadeia de conexão.  
  
### <a name="code"></a>Código  
  
```  
use AdventureWorks  
CREATE TABLE ColdCalling  
(  
ID int IDENTITY(1,1) PRIMARY KEY,  
[Date] date,  
[Time] time,  
PositiveFirstName nvarchar(50) SPARSE,  
PositiveLastName nvarchar(50) SPARSE,  
SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
);  
GO  
  
INSERT ColdCalling ([Date], [Time])  
VALUES ('10-13-09','07:05:24')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:00:24', 'AA', 'B')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:15:00', 'CC', 'DD')  
GO  
```  
  
### <a name="code"></a>Código  
  
```  
import java.sql.*;  
  
import javax.xml.parsers.DocumentBuilder;  
import javax.xml.parsers.DocumentBuilderFactory;  
  
import org.xml.sax.InputSource;  
  
import java.io.StringReader;  
  
import org.w3c.dom.Document;  
import org.w3c.dom.Node;  
import org.w3c.dom.NodeList;  
  
public class SparseColumns {  
  
   public static void main(String args[]) {  
      final String connectionUrl = "jdbc:sqlserver://my_server;databaseName=AdventureWorks;integratedSecurity=true;";  
  
      Connection conn = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         conn = DriverManager.getConnection(connectionUrl);  
  
         stmt = conn.createStatement();  
         // Determine the column set column  
         String columnSetColName = null;  
         String strCmd = "SELECT name FROM sys.columns WHERE object_id=(SELECT OBJECT_ID('ColdCalling')) AND is_column_set = 1";  
         rs = stmt.executeQuery(strCmd);  
  
         if (rs.next()) {  
            columnSetColName = rs.getString(1);  
            System.out.println(columnSetColName + " is the column set column!");  
         }  
         rs.close();  
  
         rs = null;   
  
         strCmd = "SELECT * FROM ColdCalling";  
         rs = stmt.executeQuery(strCmd);  
  
         // Iterate through the result set  
         ResultSetMetaData rsmd = rs.getMetaData();  
  
         DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();  
         DocumentBuilder db = dbf.newDocumentBuilder();  
         InputSource is = new InputSource();  
         while (rs.next()) {  
            // Iterate through the columns  
            for (int i = 1; i <= rsmd.getColumnCount(); ++i) {  
               String name = rsmd.getColumnName(i);  
               String value = rs.getString(i);  
  
               // If this is the column set column  
               if (name.equalsIgnoreCase(columnSetColName)) {  
                  System.out.println(name);  
  
                  // Instead of printing the raw XML, parse it  
                  if (value != null) {  
                     // Add artificial root node "sparse" to ensure XML is well formed  
                     String xml = "<sparse>" + value + "</sparse>";  
  
                     is.setCharacterStream(new StringReader(xml));  
                     Document doc = db.parse(is);  
  
                     // Extract the NodeList from the artificial root node that was added  
                     NodeList list = doc.getChildNodes();  
                     // This is the <sparse> node  
                     Node root = list.item(0);   
                     // These are the xml column nodes  
                     NodeList sparseColumnList = root.getChildNodes();   
  
                     // Iterate through the XML document  
                     for (int n = 0; n < sparseColumnList.getLength(); ++n) {  
                        Node sparseColumnNode = sparseColumnList.item(n);  
                        String columnName = sparseColumnNode.getNodeName();  
                        // Note that the column value is not in the sparseColumNode, it is the value of the first child of it  
                        Node sparseColumnValueNode = sparseColumnNode.getFirstChild();  
                        String columnValue = sparseColumnValueNode.getNodeValue();  
  
                        System.out.println("\t" + columnName + "\t: " + columnValue);  
                     }  
                  }  
               } else {   // Just print the name + value of non-sparse columns  
                  System.out.println(name + "\t: " + value);  
               }  
            }  
            System.out.println();//New line between rows  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      } finally {  
         if (rs != null) {  
            try {  
               rs.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
         if (stmt != null) {  
            try {  
               stmt.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
         if (conn != null) {  
            try {  
               conn.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
      }  
   }        
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

