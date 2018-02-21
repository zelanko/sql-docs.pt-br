---
title: Usar um arquivo de formato para ignorar uma coluna de tabela (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 02/13/2018
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
- skipping columns when importing
- format files [SQL Server], skipping columns
ms.assetid: 30e0e7b9-d131-46c7-90a4-6ccf77e3d4f3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8908c590ff97f09259635a407d1e37fc22956f20
ms.sourcegitcommit: aebbfe029badadfd18c46d5cd6456ea861a4e86d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="use-a-format-file-to-skip-a-table-column-sql-server"></a>Usar um arquivo de formato para ignorar uma coluna de tabela (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este artigo descreve como usar um arquivo de formato para ignorar a importação de uma coluna de tabela quando o campo não existir no arquivo de dados de origem. Um arquivo de dados poderá conter menos campos do que o número de colunas na tabela de destino – isto é, será possível ignorar a importação de uma coluna – apenas se pelo menos uma das seguintes condições for verdadeira:
-   A coluna ignorada permite valor nulo.
-   A coluna ignorada tem um valor padrão.  
  
## <a name="sample-table-and-data-file"></a>Tabela e arquivo de dados de exemplo  
 Os exemplos neste artigo esperam uma tabela chamada `myTestSkipCol` no esquema **dbo**. É possível criar esta tabela em um banco de dados de exemplo como *WideWorldImporters* ou *AdventureWorks* ou em qualquer outro banco de dados. Crie essa tabela como se segue:  
  
```sql
USE WideWorldImporters;  
GO  
CREATE TABLE myTestSkipCol   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) NULL,  
   Col3 nvarchar(50) not NULL  
   );  
GO  
```  
  
Os exemplos neste artigo também usam um arquivo de dados de exemplo, `myTestSkipCol2.dat`. Este arquivo de dados contém apenas dois campos, embora a tabela de destino contenha três colunas.

```  
1,DataForColumn3  
1,DataForColumn3  
1,DataForColumn3  
```  
  
Para importar dados em massa do `myTestSkipCol2.dat` para a tabela `myTestSkipCol`, o arquivo de formato deve mapear o primeiro campo de dados para `Col1` e mapear o segundo campo para `Col3` e ignorar `Col2`.  
  
## <a name="option-1---use-a-non-xml-format-file"></a>Opção nº 1 – Usar um arquivo de formato não XML  
É possível usar um arquivo de formato não XML para ignorar uma coluna da tabela. Há duas etapas:

1.   Use o utilitário de linha de comando **bcp** para criar um arquivo de formato não XML padrão.

2.   Modifique o arquivo de formato padrão em um editor de texto.

O arquivo de formato modificado deve mapear cada campo existente para sua coluna correspondente na tabela de destino. Ele também deve indicar qual coluna ou colunas da tabela a serem ignoradas. 
  
### <a name="step-1---create-a-default-non-xml-format-file"></a>Etapa Nº 1 – Criar um arquivo de formato não XML padrão  
Crie um arquivo de formato não XML padrão para a tabela de exemplo `myTestSkipCol` usando o seguinte comando **bcp** no prompt de comando:  
  
```cmd
bcp WideWorldImporters..myTestSkipCol format nul -f myTestSkipCol_Default.fmt -c -T  
```  
  
O comando anterior cria um arquivo de formato não XML, `myTestSkipCol_Default.fmt`. Esse arquivo de formato é denominado *arquivo de formato padrão* , pois esse é o formato gerado pelo **bcp**. Um arquivo de formato padrão descreve uma correspondência um para um entre campos de arquivo de dados e colunas de tabela.  
  
> [!IMPORTANT]  
>  Talvez seja necessário especificar o nome da instância do servidor à qual você está se conectando com o argumento `-S`. Além disso, talvez seja necessário especificar o nome de usuário e a senha com os argumentos `-U` e `-P`. Para obter mais informações, consulte [bcp Utility](../../tools/bcp-utility.md).  
  
 A captura de tela a seguir exibe os valores nesses exemplos de arquivos de formato padrão. 
  
 ![arquivo de formato não XML padrão para myTestSkipCol](../../relational-databases/import-export/media/mytestskipcol-f-c-default-fmt.gif "arquivo de formato não XML padrão para myTestSkipCol")  
  
> [!NOTE]  
>  Para obter mais informações sobre campos de arquivo de formato, consulte [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
### <a name="step-2---modify-a-non-xml-format-file"></a>Etapa nº 2 – Modificar um arquivo de formato não XML  
Há duas alternativas para se modificar um arquivo de dados não XML padrão. Ambas indicam que o campo de dados não existe no arquivo de dados e que nenhum dado deve ser inserido na coluna de tabela correspondente.

Para ignorar uma coluna de tabela, edite o arquivo de formato não XML padrão e modifique o arquivo, recorrendo a um dos seguintes métodos alternativos:  

#### <a name="option-1---remove-the-row"></a>Opção Nº 1 – Remover a linha
O método preferencial para ignorar uma coluna envolve três etapas básicas.

1.   Primeiro, exclua qualquer linha do arquivo de formato que descreva um campo ausente do arquivo de dados de origem.
2.   Então, reduza o valor da "Ordem do campo de arquivo host" de cada linha do arquivo de formato que segue uma linha excluída. A meta são valores sequenciais "Ordem do campo de arquivo host", de 1 a *n*que reflitam a posição atual de cada campo de dados no arquivo de dados.
3.   Finalmente, reduza o valor no campo "Número de colunas" para refletir o número real de campos no arquivo de dados.  
  
O exemplo a seguir foi baseado no arquivo de formato padrão para a tabela `myTestSkipCol`, criado anteriormente neste artigo, em "Criando um arquivo de formato não XML padrão". Este arquivo de formato modificado mapeia o primeiro campo de dados para a `Col1`, ignora a `Col2`e mapeia o segundo campo de dados para a `Col3`. A linha da `Col2` foi excluída. A delimitação após o primeiro campo também foi alterada de `\t` para `,`.
  
```  
14.0  
2  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
```  
  
#### <a name="option-2---modify-the-row-definition"></a>Opção Nº 2 – Modificar a definição de linha

Como alternativa para ignorar uma coluna de tabela, é possível modificar a definição da linha do arquivo de formato que corresponde à coluna de tabela. Nessa linha do arquivo de formato, os valores "comprimento do prefixo", "comprimento dos dados do arquivo host" e "ordem da coluna do servidor" devem ser definidos como 0. Além disso, o campos "terminador" e "agrupamento de colunas" devem ser definidos como "" (NULO).  
  
O valor "nome da coluna de servidor" requer uma cadeia de caracteres não vazia, embora o nome real da coluna não seja necessário. Os campos de formato restantes requerem seus valores padrão.  
  
O exemplo a seguir também é derivado do arquivo de formato padrão da tabela `myTestSkipCol` .  
  
```  
14.0  
3  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       0       ""       0     Col2         ""  
3       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
```  
  
### <a name="examples-with-a-non-xml-format-file"></a>Exemplos com um arquivo de formato não XML 
Os exemplos a seguir também são baseados na tabela de exemplo `myTestSkipCol` e no arquivo de dados de exemplo `myTestSkipCol2.dat` descritos anteriormente neste artigo.  
  
#### <a name="using-bulk-insert"></a>Usando BULK INSERT  
Este exemplo funciona usando os arquivos de formato não XML modificados criados conforme descrito na seção anterior. Nesse exemplo, o nome do arquivo de formato modificado é `myTestSkipCol2.fmt`. Para usar o `BULK INSERT` para importar o arquivo de dados `myTestSkipCol2.dat` em massa, no SSMS, execute o seguinte código. Atualize os caminhos do sistema de arquivos do local dos arquivos de exemplo em seu computador.
  
```sql  
USE WideWorldImporters;  
GO  
BULK INSERT myTestSkipCol   
   FROM 'C:\myTestSkipCol2.dat'   
   WITH (FORMATFILE = 'C:\myTestSkipCol2.fmt');  
GO  
SELECT * FROM myTestSkipCol;  
GO  
```  
  
## <a name="option-2---use-an-xml-format-file"></a>Opção nº 2 – Usar um arquivo de formato XML  

-   Com `bcp` e `BULK INSERT`. Com um arquivo de formato XML, não é possível ignorar uma coluna durante a importação direta para uma tabela usando um comando **bcp** ou uma instrução `BULK INSERT`. No entanto, é possível realizar a importação para todas as colunas de uma tabela, exceto para a última. Se for preciso ignorar alguma que não a última coluna, crie uma exibição da tabela de destino que contenha apenas as colunas contidas no arquivo de dados. Depois, importe em massa os dados desse arquivo para a exibição.  
  
-   Com `OPENROWSET(BULK...)` Para usar um arquivo de formato XML para ignorar uma coluna de tabela usando `OPENROWSET(BULK...)`, é necessário fornecer uma lista de colunas explícita na lista de seleção e também na tabela de destino, como segue:  
  
    ```sql
    INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...) 
    ```
  
### <a name="step-1---create-a-default-non-xml-format-file"></a>Etapa Nº 1 – Criar um arquivo de formato não XML padrão   

Esses exemplos dos arquivos de formato XML modificados se baseiam na tabela de exemplo `myTestSkipCol` e no arquivo de dados criados anteriormente neste artigo, em "Tabela de exemplo e arquivo de dados".

O comando **bcp** a seguir cria um arquivo de formato XML padrão para a tabela `myTestSkipCol` :  
  
```cmd
bcp WideWorldImporters..myTestSkipCol format nul -f myTestSkipCol_Default.xml -c -x -T  
```  
  
O arquivo de formato não XML padrão resultante descreve uma correspondência um-para-um entre campos de arquivo de dados e colunas de tabela, da seguinte maneira:  
  
```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  Para obter informações sobre a estrutura de arquivos de formato XML, consulte [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md).  

### <a name="step-2---modify-an-xml-format-file"></a>Etapa nº 2 – Modificar um arquivo de formato XML

Aqui está o arquivo de formato XML modificado, `myTestSkipCol2.xml`, que ignora `Col2`. As entradas `FIELD` e `ROW` para `Col2` foram removidas e as entradas foram numeradas novamente. A delimitação após o primeiro campo também foi alterada de `\t` para `,`.

```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
 
### <a name="examples-with-an-xml-format-file"></a>Exemplos com um arquivo de formato XML   
Os exemplos desta seção usam a tabela de exemplo `myTestSkipCol` e o arquivo de dados de exemplo `myTestSkipCol2.dat` criados anteriormente neste artigo, em "Tabela de exemplo e arquivo de dados". Para importar os dados de `myTestSkipCol2.dat` para a tabela `myTestSkipCol` , os exemplos usam o seguinte arquivo de formato XML modificado, `myTestSkipCol2.xml`.   
  
#### <a name="using-openrowsetbulk"></a>Usando OPENROWSET(BULK...)  
O exemplo a seguir usa o provedor de conjunto de linhas em massa `OPENROWSET` e o arquivo de formato `myTestSkipCol2.xml` . O exemplo importa em massa o arquivo de dados `myTestSkipCol2.dat` para a tabela `myTestSkipCol` . A instrução contém uma lista explícita de colunas na lista de seleção e também na tabela de destino, como exigido.  
  
No SSMS, execute o seguinte código. Atualize os caminhos do sistema de arquivos do local dos arquivos de exemplo em seu computador.
  
```sql  
USE WideWorldImporters;  
GO  
INSERT INTO myTestSkipCol  
  (Col1,Col3)  
    SELECT Col1,Col3  
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',  
      FORMATFILE='C:\myTestSkipCol2.Xml'    
       ) as t1 ;  
GO  
```  
  
#### <a name="using-bulk-import-with-a-view"></a>Usando BULK IMPORT com uma exibição  
O exemplo a seguir cria a exibição `v_myTestSkipCol` na tabela `myTestSkipCol` . Essa exibição ignora a segunda coluna da tabela, `Col2`. O exemplo usa o `BULK INSERT` para importar o arquivo de dados `myTestSkipCol2.dat` para essa exibição.  
  
No SSMS, execute o seguinte código. Atualize os caminhos do sistema de arquivos do local dos arquivos de exemplo em seu computador. 
  
```sql  
USE WideWorldImporters;  
GO  

CREATE VIEW v_myTestSkipCol AS  
    SELECT Col1,Col3  
    FROM myTestSkipCol;  
GO  
  
BULK INSERT v_myTestSkipCol  
FROM 'C:\myTestSkipCol2.dat'  
WITH (FORMATFILE='C:\myTestSkipCol2.xml');  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
  
