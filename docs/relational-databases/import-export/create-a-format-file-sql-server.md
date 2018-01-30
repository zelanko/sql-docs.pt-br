---
title: Criar um arquivo de formato (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 02/23/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- format files [SQL Server], creating
ms.assetid: f680b4a0-630f-4052-9c79-d348c1076f7b
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: e4eb0b49bbf52926536293cf26cd47046329abaf
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="create-a-format-file-sql-server"></a>Criar um formato de arquivo (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Quando você importa em massa para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou exporta em massa dados de uma tabela, pode usar um arquivo de formato para um sistema flexível para gravar arquivos de dados que exigem pouca ou nenhuma edição para ficar em conformidade com outros formatos de dados ou para ler arquivos de dados de outros programas de software.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a dois tipos de arquivo de formato: XML e não XML. O formato não XML é o formato original com suporte em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Geralmente, arquivos de formato XML e não XML são intercambiáveis. Entretanto, recomendamos que você use a sintaxe XML para novos arquivos de formato porque eles oferecem diversas vantagens em relação aos arquivos de formato não XML.  
  
> [!NOTE]  
>  A versão do utilitário **bcp** (Bcp.exe) usada para ler um arquivo de formato deve ser igual ou posterior à versão usada para criar o arquivo de formato. Por exemplo, o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]**bcp** pode ler um arquivo de formato da versão 10.0, que é gerado pelo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]**bcp**, mas o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]**bcp** não pode ler um arquivo de formato da versão 11.0, que é gerado pelo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]**bcp**.  
  
 Este tópico descreve como usar o [utilitário bcp](../../tools/bcp-utility.md) para criar um arquivo de formato para uma tabela específica. O arquivo de formato se baseia na opção do tipo de dados especificada (**-n**, **-c**, **-w**ou **-N**) e nos delimitadores de exibição ou tabela.  
  
## <a name="creating-a-non-xml-format-file"></a>Criando um arquivo de formato não XML  
 Para usar um comando **bcp** para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados. A opção **format** também exige a opção **-f** , como:  
  
 **bcp** *table_or_view* **format** nul **-f***format_file_name*  
  
> [!NOTE]  
>  Para diferenciar um arquivo de formato não XML recomendamos que você use .fmt como a extensão de nome de arquivo, por exemplo, MyTable.fmt.  
  
 Para obter informações sobre a estrutura e os campos dos arquivos de formato não XML, veja [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
### <a name="examples"></a>Exemplos  
 Esta seção contém os seguintes exemplos que mostram como usar comandos **bcp** para criar um arquivo de formato não XML:  
  
-   A. Criando um arquivo de formato não XML para dados nativos  
  
-   B. Criando um arquivo de formato não XML para dados de caracteres  
  
-   C. Criando um arquivo de formato não XML para dados nativos Unicode  
  
-   D. Criando um arquivo de formato não XML para dados de caracteres Unicode  
  
-   F. Usando um formato de arquivo com a opção de página de código  
  
 Os exemplos usam a tabela `HumanResources.Department` no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . A tabela `HumanResources.Department` contém quatro colunas: `DepartmentID`, `Name`, `GroupName`e `ModifiedDate`.  
  
#### <a name="a-creating-a-non-xml-format-file-for-native-data"></a>A. Criando um arquivo de formato não XML para dados nativos  
 O exemplo a seguir cria um arquivo de formato XML, `Department-n.xml`, para a tabela [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]`HumanResources.Department` . O arquivo de formato usa tipos de dados nativos. O conteúdo do arquivo de formato gerado é apresentado após o comando.  
  
 O comando **bcp** contém os qualificadores a seguir.  
  
|Qualificadores|Description|  
|----------------|-----------------|  
|**formatnul-f** *format_file*|Especifica o arquivo de formato não XML.|  
|**-n**|Especifica tipos de dados nativos.|  
|**-T**|Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para o logon ser efetuado com êxito.|  
  
 No prompt de comando do Windows, digite o seguinte comando `bcp` :  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -T -n -f Department-n.fmt  
```  
  
 O arquivo de formato gerado, `Department-n.fmt`, contém as seguintes informações:  
  
```  
12.0  
4  
1  SQLSMALLINT   0       2       ""   1     DepartmentID         ""  
2  SQLNCHAR      2       100     ""   2     Name                 SQL_Latin1_General_CP1_CI_AS  
3  SQLNCHAR      2       100     ""   3     GroupName            SQL_Latin1_General_CP1_CI_AS  
4  SQLDATETIME   0       8       ""   4     ModifiedDate         ""  
```  
  
 Para obter mais informações, veja [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
#### <a name="b-creating-a-non-xml-format-file-for-character-data"></a>B. Criando um arquivo de formato não XML para dados de caracteres  
 O exemplo a seguir cria um arquivo de formato XML, `Department.fmt`, para a tabela [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]`HumanResources.Department` . O arquivo de formato usa formatos de dados de caracteres e um terminador de campo não padrão (`,`). O conteúdo do arquivo de formato gerado é apresentado após o comando.  
  
 O comando **bcp** contém os qualificadores a seguir.  
  
|Qualificadores|Description|  
|----------------|-----------------|  
|**formatnul-f** *format_file*|Especifica um arquivo de formato não XML.|  
|**-c**|Especifica dados de caracteres.|  
|**-T**|Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para o logon ser efetuado com êxito.|  
  
 No prompt de comando do Windows, digite o seguinte comando `bcp` :  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -c -f Department-c.fmt -T  
```  
  
 O arquivo de formato gerado, `Department-c.fmt`, contém as seguintes informações:  
  
```  
12.0  
4  
1  SQLCHAR       0       7       "\t"     1     DepartmentID            ""  
2  SQLCHAR       0       100     "\t"     2     Name                    SQL_Latin1_General_CP1_CI_AS  
3  SQLCHAR       0       100     "\t"     3     GroupName               SQL_Latin1_General_CP1_CI_AS  
4  SQLCHAR       0       24      "\r\n"   4     ModifiedDate            ""  
```  
  
 Para obter mais informações, veja [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
#### <a name="c-creating-a-non-xml-format-file-for-unicode-native-data"></a>C. Criando um arquivo de formato não XML para dados nativos Unicode  
 Para criar um arquivo de formato não XML para dados nativos Unicode para a tabela `HumanResources.Department`, use o seguinte comando:  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -T -N -f Department-n.fmt  
```  
  
 Para obter mais informações sobre como usar dados nativos Unicode, veja [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).  
  
#### <a name="d-creating-a-non-xml-format-file-for-unicode-character-data"></a>D. Criando um arquivo de formato não XML para dados de caracteres Unicode  
 Para criar um arquivo de formato não XML para dados de caracteres Unicode para a tabela `HumanResources.Department` que usa terminadores padrão, utilize o seguinte comando:  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -T -w -f Department-w.fmt  
```  
  
 Para obter mais informações sobre como usar dados de caractere Unicode, veja [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).  
  
#### <a name="f-using-a-format-file-with-the-code-page-option"></a>F. Usando um formato de arquivo com a opção de página de código  
Se você criar um arquivo de formato usando o comando bcp (isto é, usando `bcp format`), as informações sobre o agrupamento/página de código serão gravadas no arquivo de formato.   
O arquivo de formato de exemplo a seguir, para uma tabela com 5 colunas, inclui o agrupamento.  
  
```  
13.0  
5  
1  SQLCHAR         0       0       "**\t**"         1     c_0          Cyrillic_General_CS_AS  
2  SQLCHAR         0       0       "**\t**"         2     c_1          Cyrillic_General_CS_AS  
3  SQLCHAR         0       3000    "**\t**"         3     c_2          Cyrillic_General_CS_AS  
4  SQLCHAR         0       5       "**\t**"         4     c_3          ""  
5  SQLCHAR         0       41      "!!!\r\r\n"      5     c_4          ""  
  
```  
  
 Se você tentar importar dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando `bcp in –c –C65001 –f format_file` ...” ou “`BULK INSERT`/`OPENROWSET` … `FORMATFILE='format_file' CODEPAGE=65001` …”, as informações sobre agrupamento/página de código terão prioridade sobre a opção 65001.  
Portanto, se você gerar um arquivo de formato, você deverá excluir manualmente as informações de agrupamento do arquivo de formato gerado antes de iniciar a importação de dados de volta para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
A seguir, um exemplo do formato de arquivo sem as informações de agrupamento.  
  
```  
13.0  
5  
1  SQLCHAR         0       0       "**\t**"         1     c_0              ""  
2  SQLCHAR         0       0       "**\t**"         2     c_1              ""  
3  SQLCHAR         0       3000    "**\t**"         3     c_2              ""  
4  SQLCHAR         0       5       "**\t**"         4     c_3              ""  
5  SQLCHAR         0       41      "!!!\r\r\n"      5     c_4              ""  
```  
  
## <a name="creating-an-xml-format-file"></a>Criando um arquivo de formato XML  
 Para usar um comando **bcp** para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados. A opção **format** sempre exige a opção **-f** e, para criar um arquivo de formato XML, é necessário especificar também a opção **-x** como:  
  
 **bcp** *table_or_view* **format nul-f** *format_file_name* **-x**  
  
> [!NOTE]  
>  Para diferenciar um arquivo de formato XML, recomendamos que você use .xml como a extensão de nome de arquivo, por exemplo, MyTable.xml.  
  
 Para obter informações sobre a estrutura e os campos de arquivos de formato XML, veja [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md).  
  
### <a name="examples"></a>Exemplos  
 Esta seção contém os seguintes exemplos que mostram como usar comandos **bcp** para criar um arquivo de formato XML:  
  
-   A. Criando um arquivo de formato XML para dados de caracteres  
  
-   B. Criando um arquivo de formato XML para dados nativos  
  
 Os exemplos usam a tabela `HumanResources.Department` no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . A tabela `HumanResources.Department` contém quatro colunas: `DepartmentID`, `Name`, `GroupName`e `ModifiedDate`.  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBdesc](../../includes/sssampledbdesc-md.md)]  
  
#### <a name="a-creating-an-xml-format-file-for-character-data"></a>A. Criando um arquivo de formato XML para dados de caracteres  
 O exemplo a seguir cria um arquivo de formato XML, `Department.xml`, para a tabela [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]`HumanResources.Department` . O arquivo de formato usa formatos de dados de caracteres e um terminador de campo não padrão (`,`). O conteúdo do arquivo de formato gerado é apresentado após o comando.  
  
 O comando **bcp** contém os qualificadores a seguir.  
  
|Qualificadores|Description|  
|----------------|-----------------|  
|**formatnul-f** *format_file* **-x**|Especifica o arquivo de formato XML.|  
|**-c**|Especifica dados de caracteres.|  
|**-t** `,`|Especifica uma vírgula (**,**) como terminador de campo.<br /><br /> Se o arquivo de dados usar o terminador de campo padrão (`\t`), a opção **-t** será desnecessária.|  
|**-T**|Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para o logon ser efetuado com êxito.|  
  
 No prompt de comando do Windows, digite o seguinte comando `bcp` :  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -c -x -f Department-c..xml –t, -T  
```  
  
 O arquivo de formato gerado, `Department-c.xml`, contém os seguintes elementos XML:  
  
```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="24"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="DepartmentID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="GroupName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="ModifiedDate" xsi:type="SQLDATETIME"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 Para obter informações sobre a sintaxe deste arquivo de formato XML, veja [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md). Para obter informações sobre dados de caractere, veja [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).  
  
#### <a name="b-creating-an-xml-format-file-for-native-data"></a>B. Criando um arquivo de formato XML para dados nativos  
 O exemplo a seguir cria um arquivo de formato XML, `Department-n.xml`, para a tabela `HumanResources.Department` . O arquivo de formato usa tipos de dados nativos. O conteúdo do arquivo de formato gerado é apresentado após o comando.  
  
 O comando **bcp** contém os qualificadores a seguir.  
  
|Qualificadores|Description|  
|----------------|-----------------|  
|**formatnul-f** *format_file* **-x**|Especifica o arquivo de formato XML.|  
|**-n**|Especifica tipos de dados nativos.|  
|**-T**|Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para o logon ser efetuado com êxito.|  
  
 No prompt de comando do Windows, digite o seguinte comando `bcp` :  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -x -f Department-n..xml -n -T  
```  
  
 O arquivo de formato gerado, `Department-n.xml`, contém os seguintes elementos XML:  
  
```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="NativeFixed" LENGTH="2"/>  
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="NativeFixed" LENGTH="8"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="DepartmentID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="GroupName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="ModifiedDate" xsi:type="SQLDATETIME"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 Para obter informações sobre a sintaxe deste arquivo de formato XML, veja [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md). Para obter informações sobre como usar dados nativos, veja [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).  
  
## <a name="mapping-data-fields-to-table-columns"></a>Mapeando campos de dados para colunas de tabelas  
 Como criado pelo **bcp**, um arquivo de formato descreve todas as colunas da tabela em ordem. Você pode modificar um arquivo de formato para reorganizar ou omitir linhas de tabela. Isso permite a personalização de um arquivo de formato cujos campos não são mapeados diretamente para as colunas da tabela. Para obter mais informações, consulte os tópicos a seguir:  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  
  
