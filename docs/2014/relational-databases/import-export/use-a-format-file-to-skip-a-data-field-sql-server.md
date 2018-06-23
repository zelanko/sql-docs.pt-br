---
title: Usar um arquivo de formato para ignorar um campo de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a60d4d668cb9c7d7d13a60a12df1057b24eea465
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117675"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>Usar um arquivo de formato para ignorar um campo de dados (SQL Server)
  Um arquivo de dados pode conter mais campos do que o número de colunas na tabela. Este tópico descreve como modificar arquivos de formato XML e não XML para acomodar um arquivo de dados com mais campos, mapeando as colunas de tabela para os campos de dados correspondentes e ignorando os campos extras.  
  
> [!NOTE]  
>  Um arquivo de formato XML ou não XML pode ser usado para a importação em massa um arquivo de dados para a tabela usando um comando **bcp**, uma instrução BULK INSERT ou INSERT... Instrução SELECT * FROM OPENROWSET(BULK...). Para obter mais informações, veja [Usar um arquivo de formato para importação de dados em massa &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md).  
  
## <a name="sample-data-file-and-table"></a>Tabela e arquivo de dados de exemplo  
 Os exemplos de arquivos de formato modificados neste tópico baseiam-se na tabela e no arquivo de dados a seguir.  
  
### <a name="sample-table"></a>Tabela de exemplo  
 Os exemplos requerem que uma tabela denominada `myTestSkipField` seja criada no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] no esquema `dbo` . Para criar essa tabela, no Editor de Consultas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] execute o seguinte código:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipField   
   (  
   PersonID smallint,  
   FirstName nvarchar(50) ,  
   LastName nvarchar(50)   
   );  
GO  
```  
  
### <a name="sample-data-file"></a>Arquivo de dados de exemplo  
 O arquivo de dados `myTestSkipField-c.dat`contém os seguintes registros:  
  
```  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
```  
  
 Para importar em massa dados de `myTestSkipField-c.dat` para a tabela `myTestSkipField` , o arquivo de formato deve fazer o seguinte:  
  
-   Mapear o primeiro campo de dados para a primeira coluna, `PersonID`.  
  
-   Ignorar o segundo campo de dados.  
  
-   Mapear o terceiro campo de dados para a segunda coluna, `FirstName`.  
  
-   Mapear o quarto campo de dados para a terceira coluna, `LastName`.  
  
## <a name="non-xml-format-file-for-more-data-fields"></a>Arquivo de formato não XML para mais campos de dados  
 O arquivo de formato a seguir, `myTestSkipField.fmt`, mapeia os campos em `myTestSkipField-c.dat` para as colunas da tabela `myTestSkipField`. O arquivo de formato usa o formato de dados de caracteres. Ignorar um mapeamento de coluna requer a alteração do valor da ordem da coluna para 0, como mostrado para a coluna `ExtraField` no arquivo de formato.  
  
 O arquivo de formato `myTestSkipField.fmt` contém as seguintes informações:  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     PersonID               ""  
2       SQLCHAR       0       100       ","    0     ExtraField             SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   3     LastName               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  Para obter informações sobre a sintaxe dos arquivos de formato não XML, veja [Arquivos de formato não XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `INSERT ... SELECT * FROM OPENROWSET(BULK...)` utilizando o arquivo de formato `myTestSkipField.fmt` . O exemplo importa em massa o arquivo de dados `myTestSkipField-c.dat` para a tabela `myTestSkipField` . Para criar a tabela e o arquivo de dados de exemplo, consulte "Tabela e arquivo de dados de exemplo", anteriormente neste tópico.  
  
 No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , execute o seguinte código:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
   SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.fmt'    
       ) AS t1;  
GO   
```  
  
## <a name="xml-format-file-for-more-data-fields"></a>Arquivo de formato XML para mais campos de dados  
 O arquivo de formato apresentado neste exemplo tem base em outro arquivo de formato, `myTestSkipField.xml`, que usa formato de dados de caracteres sempre e cujos campos correspondem exatamente em número e ordem às colunas na tabela `myTestSkipField`. Para exibir o conteúdo desse arquivo de formato, veja [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
 O arquivo de formato a seguir, `myTestSkipField.xml`, mapeia os campos em `myTestSkipField-c.dat` para as colunas da tabela `myTestSkipField`. O arquivo de formato usa o formato de dados de caracteres.  
  
 O arquivo de formato `myTestSkipField.xml` contém as seguintes informações:  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
### <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `INSERT ... SELECT * FROM OPENROWSET(BULK...)` utilizando o arquivo de formato `myTestSkipField.Xml` . O exemplo importa em massa o arquivo de dados `myTestSkipField-c.dat` para a tabela `myTestSkipField` . Para criar a tabela e o arquivo de dados de exemplo, consulte "Tabela e arquivo de dados de exemplo", anteriormente neste tópico.  
  
 No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute o seguinte código:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
  SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.xml'    
       ) AS t1;  
GO  
  
```  
  
> [!NOTE]  
>  Para obter informações sobre a sintaxe do esquema XML e exemplos adicionais de arquivos de formato XML, veja [Arquivos de formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
