---
title: Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 26db59ba5dbfc6f7be8d827a86dabb1cdd845d03
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371528"
---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados (SQL Server)
  Um arquivo de dados pode conter campos organizados em uma ordem diferente das colunas correspondentes na tabela. Este tópico apresenta arquivos de formato não XML e XML que foram modificados para acomodar um arquivo de dados cujos campos são organizados em uma ordem diferente das colunas da tabela. O arquivo de formato modificado mapeia os campos de dados para as colunas da tabela correspondentes.  
  
> [!NOTE]  
>  Um arquivo de formato XML ou não XML pode ser usado para importar em massa um arquivo de dados para a tabela usando um comando do **bcp**, uma instrução BULK INSERT ou INSERT... Instrução SELECT * FROM OPENROWSET(BULK...). Para obter mais informações, veja [Usar um arquivo de formato para importação de dados em massa &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md).  
  
## <a name="sample-table-and-data-file"></a>Tabela e arquivo de dados de exemplo  
 Os exemplos de arquivos de formato modificados neste tópico baseiam-se na tabela e no arquivo de dados a seguir.  
  
### <a name="sample-table"></a>Tabela de exemplo  
 Os exemplos neste tópico exigem a criação de uma tabela denominada `myTestOrder` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] sob o esquema `dbo`. Para criar essa tabela, no Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute o seguinte código:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestOrder   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) ,  
   Col3 nvarchar(50) ,   
   Col4 nvarchar(50)   
   );  
GO  
  
```  
  
### <a name="data-file"></a>Arquivo de dados  
 O arquivo de dados `myTestOrder-c.txt` contém os seguintes registros:  
  
```  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
  
```  
  
 Para importar dados em massa do `myTestSkipCol2-c.dat` para a tabela `myTestSkipCol`, o arquivo de formato deve mapear o primeiro campo de dados para `Col3`, o segundo campo de dados para `Col2`, o terceiro campo de dados para `Col1`e o quarto campo de dados para `Col4`.  
  
## <a name="using-a-non-xml-format-file"></a>Usando um arquivo de formato não XML  
 Você pode alterar a ordem de um mapeamento de coluna alterando o valor da ordem da coluna para indicar a posição do campo de dados correspondente.  
  
 O exemplo de arquivo de formato não XML a seguir apresenta um arquivo de formato, `myTestOrder.fmt`, que mapeia os campos no `myTestOrder-c.txt` para as colunas da tabela `myTestOrder`. Para obter informações sobre como criar o arquivo de dados e a tabela, consulte "Tabela e arquivo de dados de exemplo" anteriormente neste tópico. O arquivo de formato usa o formato de dados de caracteres.  
  
 Ele contém as seguintes informações:  
  
```  
9.0  
4  
1       SQLCHAR       0       100     ","     3     Col3               SQL_Latin1_General_CP1_CI_AS  
2       SQLCHAR       0       100     ","     2     Col2               SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       7       ","     1     Col1               ""  
4       SQLCHAR       0       100     "\r\n"  4     Col4               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  Para obter mais informações sobre o layout dos arquivos de formato não XML, veja [Arquivos de formato não XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="example"></a>Exemplo  
 O exemplo abaixo usa uma instrução `BULK INSERT` para importar dados em massa do arquivo de dados `myTestOrder-c.txt` para a tabela de exemplo `myTestOrder` usando o arquivo de formato não XML `myTestOrder.fmt`.  
  
 No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute:  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestOrder  
FROM 'C:\myTestOrder-c.txt'   
WITH (formatfile='C:\myTestOrder.fmt');  
GO  
  
```  
  
## <a name="using-an-xml-format-file"></a>Usando um arquivo de formato XML   
 O exemplo de arquivo de formato não XML a seguir apresenta um arquivo de formato, `myTestOrder.xml`, que mapeia os campos no `myTestOrder-c.txt` para as colunas da tabela `myTestOrder`. Para obter informações sobre como criar o arquivo de dados e a tabela, consulte "Tabela e arquivo de dados de exemplo" anteriormente neste tópico.  
  
 O arquivo de formato `myTestOrder.xml` contém as seguintes informações:  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="3" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="1" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
  
```  
  
> [!NOTE]  
>  Para obter informações sobre a sintaxe do esquema XML e exemplos adicionais de arquivos de formato XML, veja [Arquivos de formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="example"></a>Exemplo  
 O exemplo abaixo usa o provedor de conjuntos de linhas em massa `OPENROWSET` para importar dados do arquivo de dados `myTestOrder-c.txt` para a tabela de exemplo `myTestOrder` usando o arquivo de formato XML `myTestOrder.xml`. A instrução `INSERT... SELECT` especifica a lista de colunas na lista de seleção.  
  
 No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute o seguinte código:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestOrder   
  SELECT Col1, Col2, Col3, Col4  
      FROM  OPENROWSET(BULK  'C:\myTestOrder-c.txt',  
      FORMATFILE='C:\myTestOrder.Xml'    
       ) AS t1;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  
