---
title: Exemplos de importação e exportação em massa de documentos XML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- field terminators [SQL Server]
- bulk importing [SQL Server], data formats
- row terminators [SQL Server]
- OPENROWSET function, XML bulk load
- terminators [SQL Server]
- bulk exporting [SQL Server], data formats
- XML bulk load [SQL Server]
ms.assetid: dff99404-a002-48ee-910e-f37f013d946d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9d573faebbbfcaf8a501a80aa093584af7fa0307
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515848"
---
# <a name="examples-of-bulk-import-and-export-of-xml-documents-sql-server"></a>Exemplos de importação e exportação em massa de documentos XML (SQL Server)
    
##  <a name="top"></a> Você pode importar documentos XML em massa em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados ou em massa exportá-los de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. Este tópico fornece exemplos de ambas as operações.  
  
 Para importar dados em massa de em arquivo de dados para uma tabela ou exibição não particionada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode usar o seguinte:  
  
-   utilitário**bcp**   
  
     Você também pode usar o utilitário **bcp** para exportar dados de qualquer lugar de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que a instrução SELECT funcionar, incluindo exibições particionadas.  
  
-   BULK INSERT  
  
-   INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
 Para obter mais informações, consulte [importar e exportar em massa dados usando o utilitário bcp &#40;SQL Server&#41; ](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md) e [importar dados em massa usando BULK INSERT ou OPENROWSET&#40;BULK... &#41; &#40;Do SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos são:  
  
-   A. [IMPORTAÇÃO de dados XML como um fluxo de bytes binários](#binary_byte_stream)  
  
-   b. [Importação de dados XML em uma linha existente](#existing_row)  
  
-   C. [Importação em massa dados XML de um arquivo que contém um DTD](#file_contains_dtd)  
  
-   D. [Especificação do terminador de campo explicitamente usando um arquivo de formato](#field_terminator_in_format_file)  
  
-   E. [Exportar dados XML em massa](#bulk_export_xml_data)  
  
###  <a name="binary_byte_stream"></a> A. Importação em massa de dados XML como um fluxo de bytes binários  
 Ao importar dados XML em massa de um arquivo que contém uma declaração de codificação que você deseja aplicar, especifique a opção SINGLE_BLOB na cláusula OPENROWSET (BULK…). A opção SINGLE_BLOB assegura que o analisador XML no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importe os dados de acordo com o esquema de codificação especificado na declaração XML.  
  
#### <a name="sample-table"></a>Tabela de exemplo  
 Para testar o exemplo A, você deve criar a tabela de exemplo `T`.  
  
```  
USE tempdb  
CREATE TABLE T (IntCol int, XmlCol xml);  
GO  
```  
  
#### <a name="sample-data-file"></a>Arquivo de dados de exemplo  
 Antes de poder executar o exemplo A, você deve criar um arquivo codificado UTF-8 (`C:\SampleFolder\SampleData3.txt`) que contenha a seguinte instância de exemplo que especifica o esquema de codificação `UTF-8` .  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
<Root>  
          <ProductDescription ProductModelID="5">  
             <Summary>Some Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-a"></a>Exemplo A  
 Esse exemplo usa a opção `SINGLE_BLOB` em uma instrução `INSERT ... SELECT * FROM OPENROWSET(BULK...)` para importar dados de um arquivo nomeado como `SampleData3.txt` e inserir uma instância XML na tabela com uma coluna, tabela de exemplo `T`.  
  
```  
INSERT INTO T(XmlCol)  
SELECT * FROM OPENROWSET(  
   BULK 'c:\SampleFolder\SampleData3.txt',  
   SINGLE_BLOB) AS x;  
```  
  
#### <a name="remarks"></a>Comentários  
 Usando SINGLE_BLOB nesse caso, você pode evitar uma desigualdade entre a codificação do documento XML (como especificado pela declaração de codificação XML) e a cadeia de caracteres da página de código implícita pelo servidor.  
  
 Se você usar tipos de dados NCLOB ou CLOB e executar em uma página de código ou conflito de código, você deve adotar um dos seguintes procedimentos:  
  
-   Remova a declaração XML para importar o conteúdo do arquivo de dados XML com êxito.  
  
-   Especifique uma página de código na opção CODEPAGE da consulta que corresponda ao esquema de codificação usado na declaração XML.  
  
-   Faça a correspondência ou resolva as definições de ordenação do banco de dados com um esquema de codificação XML não Unicode.  
  
 [&#91;Início&#93;](#top)  
  
###  <a name="existing_row"></a> B. Importação em massa de dados XML em uma linha existente  
 Este exemplo usa o provedor de conjunto de linhas em massa `OPENROWSET` para adicionar uma instância XML a uma linha ou linhas existentes na tabela de exemplo `T`.  
  
> [!NOTE]  
>  Para executar esse exemplo, você deve completar o teste de script fornecido no exemplo A, que cria a tabela `tempdb.dbo.T` e importa em massa os dados do `SampleData3.txt`.  
  
#### <a name="sample-data-file"></a>Arquivo de dados de exemplo  
 O exemplo B usa uma versão modificada do arquivo de dados de exemplo `SampleData3.txt` do exemplo anterior. Para executar esse exemplo, modifique o conteúdo desse arquivo como indicado abaixo:  
  
```  
<Root>  
          <ProductDescription ProductModelID="10">  
             <Summary>Some New Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-b"></a>Exemplo B  
  
```  
-- Query before update shows initial state of XmlCol values.  
SELECT * FROM T  
UPDATE T  
SET XmlCol =(  
SELECT * FROM OPENROWSET(  
   BULK 'C:\SampleFolder\SampleData3.txt',  
           SINGLE_BLOB  
) AS x  
)  
WHERE IntCol = 1;  
GO  
```  
  
 [&#91;Início&#93;](#top)  
  
###  <a name="file_contains_dtd"></a> C. Importação em massa de dados XML de um arquivo que contém um DTD  
  
> [!IMPORTANT]  
>  Recomendamos não habilitar o suporte a definições do tipo de documento (DTDs, Document Type Definitions) se não for necessário em seu ambiente XML. Ativar o suporte a DTD aumenta a área da superfície atacável de seu servidor e pode expô-lo a um ataque de negação de serviço. Caso seja necessário habilitar o suporte a DTD, você pode reduzir esse risco de segurança processando somente documentos XML confiáveis.  
  
 Durante uma tentativa de usar um comando [bcp](../../tools/bcp-utility.md) para importar dados XML de um arquivo que contém um DTD, pode ocorrer um erro semelhante ao descrito abaixo:  
  
 "SQLState = 42000, NativeError = 6359"  
  
 "Erro = [Microsoft][SQL Server Native Client][ SQL Server]Não é permitida a análise de XML com DTDs de subconjunto interno. Use CONVERT com a opção de estilo 2 para habilitar o suporte a DTD de subconjunto interno limitado."  
  
 "Falha na cópia BCP %s"  
  
 Para resolver esse problema, você pode importar dados XML de um arquivo de dados que contém um DTD usando a função `OPENROWSET(BULK...)` e especificando a opção `CONVERT` na cláusula de comando `SELECT` . A sintaxe básica do comando é:  
  
 `INSERT ... SELECT CONVERT(...) FROM OPENROWSET(BULK...)`  
  
#### <a name="sample-data-file"></a>Arquivo de dados de exemplo  
 Antes de poder testar esse exemplo de importação em massa, crie um arquivo (`C:\temp\Dtdfile.xml`) que contém a seguinte instância de exemplo:  
  
```  
<!DOCTYPE DOC [<!ATTLIST elem1 attr1 CDATA "defVal1">]><elem1>January</elem1>  
```  
  
#### <a name="sample-table"></a>Tabela de exemplo  
 O exemplo que C usa a tabela de exemplo `T1` , criada pela seguinte instrução `CREATE TABLE` :  
  
```  
USE tempdb;  
CREATE TABLE T1(XmlCol xml);  
GO  
```  
  
#### <a name="example-c"></a>Exemplo C  
 Este exemplo usa `OPENROWSET(BULK...)` e especifica a opção `CONVERT` na cláusula `SELECT` para importar os dados XML do `Dtdfile.xml` na tabela de exemplo `T1`.  
  
```  
INSERT T1  
  SELECT CONVERT(xml, BulkColumn, 2) FROM   
    OPENROWSET(Bulk 'c:\temp\Dtdfile.xml', SINGLE_BLOB) [rowsetresults];  
```  
  
 Depois que a instrução `INSERT` é executada, o DTD é eliminado do XML e armazenado na tabela `T1` .  
  
 [&#91;Início&#93;](#top)  
  
###  <a name="field_terminator_in_format_file"></a> D. Especificação do terminador de campo que usa explicitamente um arquivo de formato  
 O exemplo abaixo mostra como importar em massa o seguinte documento XML, `Xmltable.dat`.  
  
#### <a name="sample-data-file"></a>Arquivo de dados de exemplo  
 O documento em `Xmltable.dat` contém dois valores XML, um para cada linha. O primeiro valor XML é codificado com UTF-16 e o segundo valor é codificado com UTF-8.  
  
 O conteúdo deste arquivo de dados é mostrado no despejo hexadecimal abaixo:  
  
```  
FF FE 3C 00 3F 00 78 00-6D 00 6C 00 20 00 76 00  *..<.?.x.m.l. .v.*  
65 00 72 00 73 00 69 00-6F 00 6E 00 3D 00 22 00  *e.r.s.i.o.n.=.".*  
31 00 2E 00 30 00 22 00-20 00 65 00 6E 00 63 00  *1...0.". .e.n.c.*  
6F 00 64 00 69 00 6E 00-67 00 3D 00 22 00 75 00  *o.d.i.n.g.=.".u.*  
74 00 66 00 2D 00 31 00-36 00 22 00 3F 00 3E 00  *t.f.-.1.6.".?.>.*  
3C 00 72 00 6F 00 6F 00-74 00 3E 00 A2 4F 9C 76  *<.r.o.o.t.>..O.v*  
0C FA 77 E4 80 00 89 00-00 06 90 06 91 2E 9B 2E  *..w.............*  
99 34 A2 34 86 00 83 02-92 20 7F 02 4E C5 E4 A3  *.4.4..... ..N...*  
34 B2 B7 B3 B7 FE F8 FF-F8 00 3C 00 2F 00 72 00  *4.........<./.r.*  
6F 00 6F 00 74 00 3E 00-00 00 00 00 7A EF BB BF  *o.o.t.>.....z...*  
3C 3F 78 6D 6C 20 76 65-72 73 69 6F 6E 3D 22 31  *<?xml version="1*  
2E 30 22 20 65 6E 63 6F-64 69 6E 67 3D 22 75 74  *.0" encoding="ut*  
66 2D 38 22 3F 3E 3C 72-6F 6F 74 3E E4 BE A2 E7  *f-8"?><root>....*  
9A 9C EF A8 8C EE 91 B7-C2 80 C2 89 D8 80 DA 90  *................*  
E2 BA 91 E2 BA 9B E3 92-99 E3 92 A2 C2 86 CA 83  *................*  
E2 82 92 C9 BF EC 95 8E-EA 8F A4 EB 88 B4 EB 8E  *................*  
B7 EF BA B7 EF BF B8 C3-B8 3C 2F 72 6F 6F 74 3E  *.........</root>*  
00 00 00 00 7A                                   *....z*  
```  
  
#### <a name="sample-table"></a>Tabela de exemplo  
 Ao importar ou exportar um documento XML em massa, você deve usar um [terminador de campo](specify-field-and-row-terminators-sql-server.md) , que não pode aparecer em nenhum dos documentos; por exemplo, uma série de quatro nulos (`\0`) seguida pela letra `z`: `\0\0\0\0z`.  
  
 Esse exemplo mostra como usar esse terminador de campo na tabela de exemplo `xTable` . Para criar essa tabela exemplo, use a seguinte instrução `CREATE TABLE` :  
  
```  
USE tempdb;  
CREATE TABLE xTable (xCol xml);  
GO  
```  
  
#### <a name="sample-format-file"></a>Arquivo de formato de exemplo  
 O terminador de campo deve ser especificado no arquivo de formato. O exemplo D usa um arquivo de formato não XML chamado `Xmltable.fmt` que contém:  
  
```  
9.0  
1  
1       SQLBINARY     0       0       "\0\0\0\0z"    1     xCol         ""  
```  
  
 Você pode usar esse arquivo de formato para importar documentos XML em massa na tabela `xTable` usando um comando `bcp` ou uma instrução `BULK INSERT` ou `INSERT ... SELECT * FROM OPENROWSET(BULK...)` .  
  
#### <a name="example-d"></a>Exemplo D  
 Este exemplo usa o arquivo de formato `Xmltable.fmt` em uma instrução `BULK INSERT` para importar o conteúdo de um arquivo de dados XML chamado `Xmltable.dat`.  
  
```  
BULK INSERT xTable   
FROM 'C:\Xmltable.dat'  
WITH (FORMATFILE = 'C:\Xmltable.fmt');  
GO  
```  
  
 [&#91;Início&#93;](#top)  
  
###  <a name="bulk_export_xml_data"></a> E. Exportação em massa de dados XML  
 O exemplo abaixo usa o `bcp` para exportar dados XML em massa da tabela criada no exemplo anterior usando o mesmo arquivo de formato XML. No comando `bcp` abaixo, `<server_name>` e `<instance_name>` representam espaços reservados que devem ser substituídos com os valores apropriados:  
  
```  
bcp bulktest..xTable out a-wn.out -N -T -S<server_name>\<instance_name>  
```  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não salva a codificação XML quando os dados XML são persistentes no banco de dados. Portanto, a codificação original de campos XML não está disponível quando dados XML são exportados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a codificação UTF-16 ao exportar dados XML.  
  
 [&#91;Início&#93;](#top)  
  
## <a name="see-also"></a>Consulte também  
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [Cláusula SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-clause-transact-sql)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
