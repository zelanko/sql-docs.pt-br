---
title: Usar um arquivo de formato para importação em massa de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 772dbb86188bf164a2e135f7bb9b71a1cc030745
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011765"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>Usar um arquivo de formato para importação em massa de dados (SQL Server)
  Este tópico ilustra o uso de um arquivo de formato operações de importação em massa. O arquivo de formato mapeia os campos do arquivo de dados para as colunas da tabela.  Você pode usar um arquivo de formato não XML ou XML para importar dados em massa ao usar um comando **bcp** ou uma instrução BULK INSERT ou INSERT... SELECT * FROM OPENROWSET(BULK...) [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  Para trabalhar com um arquivo de dados de caractere Unicode, todos os campos de entrada devem ser cadeias de caracteres de texto Unicode (isto é, sejam cadeias de caracteres Unicode de tamanho fixo ou terminadas por caractere).  
  
> [!NOTE]  
>  Se você estiver familiarizado com arquivos de formato, consulte [arquivos de formato não XML &#40;SQL Server&#41; ](xml-format-files-sql-server.md) e [arquivos de formato XML &#40;do SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="format-file-options-for-bulk-import-commands"></a>Opções arquivo de formato de dados para comandos de importação em massa  
 A tabela a seguir resume a opção de arquivo de formato para cada um dos comandos de importação em massa.  
  
|Comando de carregamento em massa|Usando a opção de Arquivo de Formato|  
|------------------------|-----------------------------------|  
|BULK INSERT|FORMATFILE = '*format_file_path*'|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|FORMATFILE = '*format_file_path*'|  
|**bcp** ... **in**|**-f** *format_file*|  
  
 Para obter mais informações, consulte [Utilitário bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) ou [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Para exportar ou importar dados SQLXML em massa, use um dos tipos de dados a seguir em seu arquivo de formato: SQLCHAR ou SQLVARYCHAR (os dados são enviados na página de código do cliente ou na página de código implícita pela ordenação), SQLNCHAR ou SQLNVARCHAR (os dados são enviados como Unicode), ou SQLBINARY ou SQLVARYBIN (os dados são enviados sem nenhuma conversão).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos nesta seção ilustram como usar arquivos de formato para importar dados em massa usando o comando **bcp** e as instruções BULK INSERT e INSERT... SELECT * FROM OPENROWSET(BULK...). Antes de poder executar um dos exemplos de importação em massa, você precisa criar uma amostra de tabela, arquivo de dados e arquivo de formato.  
  
### <a name="sample-table"></a>Tabela de exemplo  
 Os exemplos requerem que uma tabela denominada **myTestFormatFiles** seja criada no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] no esquema **dbo** . Para criar esta tabela, no Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestFormatFiles (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50),  
   Col4 nvarchar(50)  
   );  
GO  
```  
  
### <a name="sample-data-file"></a>Arquivo de dados de exemplo  
 Os exemplos usam um arquivo de dados de amostra, `myTestFormatFiles-c.Dat`que contém os seguintes registros. Para criar esse arquivo de dados, no prompt de comando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, digite:  
  
```  
10,Field2,Field3,Field4  
15,Field2,Field3,Field4  
46,Field2,Field3,Field4  
58,Field2,Field3,Field4  
```  
  
### <a name="sample-format-files"></a>Arquivo de formato de exemplo  
 Alguns dos exemplos nessa seção usam um arquivo de formato XML, `myTestFormatFiles-f-x-c.Xml`e, outros exemplos usam um arquivo de formato não XML. Ambos os arquivos de formato usam formatos de dados de caracteres e um terminador de campo não padrão (,).  
  
#### <a name="the-sample-non-xml-format-file"></a>O exemplo de arquivo de formato não XML  
 O exemplo a seguir usa **bcp** para gerar um arquivo de formato XML a partir da tabela `myTestFormatFiles` . O arquivo `myTestFormatFiles.Fmt` contém as seguintes informações:  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     ","      2     Col2         SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      3     Col3         SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   4     Col4         SQL_Latin1_General_CP1_CI_AS  
```  
  
 Para usar **bcp** com a opção **format** para criar esse arquivo de formato, no prompt de comando do Windows, digite:  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -f myTestFormatFiles.Fmt -T  
  
```  
  
 Para obter mais informações sobre como criar um arquivo de formato, consulte [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
#### <a name="the-sample-xml-format-file"></a>O arquivo de formato XML de exemplo  
 O exemplo a seguir usa **bcp** para criar a geração de um arquivo de formato XML a partir da tabela `myTestFormatFiles` . O arquivo `myTestFormatFiles.Xml` contém as seguintes informações:  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 Para usar **bcp** com a opção **format** para criar esse arquivo de formato, no prompt de comando do Windows, digite:  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -x -f myTestFormatFiles.Xml -T  
```  
  
### <a name="using-bcp"></a>Usando bcp  
 O exemplo a seguir usa **bcp** para importar em massa dados do arquivo de dados `myTestFormatFiles-c.Dat` na tabela `HumanResources.myTestFormatFiles` no banco de dados de exemplo. Este exemplo usa um arquivo de formato XML, `MyTestFormatFiles.Xml`. O exemplo exclui as linhas existentes na tabela antes de importar o arquivo de dados.  
  
 No prompt de comando do Windows, digite:  
  
```  
bcp AdventureWorks2012..myTestFormatFiles in C:\myTestFormatFiles-c.Dat -f C:\myTestFormatFiles.Xml -T  
```  
  
> [!NOTE]  
>  Para obter mais informações sobre esse comando, consulte [Utilitário bcp](../../tools/bcp-utility.md).  
  
### <a name="using-bulk-insert"></a>Usando BULK INSERT  
 O exemplo a seguir usa BULK INSERT para importar em massa dados do arquivo de dados `myTestFormatFiles-c.Dat` na tabela `HumanResources.myTestFormatFiles` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. Este exemplo usa um arquivo de formato não XML, `MyTestFormatFiles.Fmt`. O exemplo exclui as linhas existentes na tabela antes de importar o arquivo de dados.  
  
 No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], execute:  
  
```  
USE AdventureWorks2012;  
GO  
DELETE myTestFormatFiles;  
GO  
BULK INSERT myTestFormatFiles   
   FROM 'C:\myTestFormatFiles-c.Dat'   
   WITH (FORMATFILE = 'C:\myTestFormatFiles.Fmt');  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
> [!NOTE]  
>  Para obter mais informações sobre esta instrução, consulte [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
### <a name="using-the-openrowset-bulk-rowset-provider"></a>Usando o Provedor de Conjuntos de Linhas em Massa OPENROWSET  
 O exemplo a seguir usa `INSERT ... SELECT * FROM OPENROWSET(BULK...)` para importar em massa dados do arquivo de dados `myTestFormatFiles-c.Dat` na tabela `HumanResources.myTestFormatFiles` no banco de dados de exemplo `AdventureWorks` . Este exemplo usa um arquivo de formato XML, `MyTestFormatFiles.Xml`. O exemplo exclui as linhas existentes na tabela antes de importar o arquivo de dados.  
  
 No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks2012;  
DELETE myTestFormatFiles;  
GO  
INSERT INTO myTestFormatFiles  
    SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestFormatFiles-c.Dat',  
      FORMATFILE='C:\myTestFormatFiles.Xml'       
      ) as t1 ;  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
 Quando você terminar de usar a tabela de amostra, pode descartá-la usando a instrução:  
  
```  
DROP TABLE myTestFormatFiles  
```  
  
> [!NOTE]  
>  Para obter mais informações sobre a cláusula OPENROWSET BULK, veja [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
## <a name="additional-examples"></a>Exemplos adicionais  
 [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
 [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
 [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Arquivos de formato não XML &#40;SQL Server&#41;](xml-format-files-sql-server.md)   
 [Arquivos de formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md)  
  
  
