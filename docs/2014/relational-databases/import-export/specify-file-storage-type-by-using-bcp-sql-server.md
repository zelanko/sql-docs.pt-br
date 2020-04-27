---
title: Especificar tipo de armazenamento do arquivo usando bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a3646aa6ef61c820ca5512203b0ff1e36894cab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011816"
---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>Especificar tipo de armazenamento de arquivo usando bcp (SQL Server)
  O *tipo de armazenamento de arquivo* descreve como são armazenados os dados no arquivo de dados. Podem ser exportados dados para um arquivo de dados como seu tipo de tabela de banco de dados (formato nativo), em sua representação de caractere (formato de caractere), ou como qualquer tipo de dados onde há suporte para conversão implícita; por exemplo, copiando um `smallint` como um `int`. Os tipos de dados definidos pelo usuário como tipos básicos são exportados.  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>Solicitação de bcp para o tipo de armazenamento de arquivo  
 Se um comando **bcp** interativo contiver a opção **in** ou **out** sem a opção do arquivo de formatos ( **-f**) ou uma opção do formato de dados ( **-n**, **-c**, **-w**ou **-N**), o comando solicitará o tipo de armazenamento de arquivos de cada campo de dados, da seguinte maneira:  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 Sua resposta para esta solicitação depende da tarefa que você executa, como segue:  
  
-   Para exportar dados em massa de uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados no armazenamento mais compacto possível (formato de dados nativo), aceite os tipos de armazenamento de arquivos padrão fornecidos pelo **bcp**. Para obter uma lista de tipos de armazenamento de arquivos nativos, digite "Tipos de Armazenamento de Arquivos Nativos", mais adiante neste tópico.  
  
-   Para agrupar dados exportados de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados no formato de caractere, especifique `char` como o tipo de armazenamento de arquivo para todas as colunas na tabela.  
  
-   Para agrupar dados importados para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um arquivo de dados, especifique o tipo de armazenamento de arquivo como `char` para tipos armazenados no formato de caractere; e para dados armazenados no formato de tipo de dados nativo, especifique um dos tipos de armazenamento de arquivo como apropriado:  
  
    |tipo de armazenamento de arquivo|Digite no prompt de comando|  
    |-----------------------|-----------------------------|  
    |`char`<sup>1</sup>|`c`[`har`]|  
    |`varchar`|`c[har]`|  
    |`nchar`|`w`|  
    |`nvarchar`|`w`|  
    |`text` <sup>2</sup>|`T`[`ext`]|  
    |`ntext2`|`W`|  
    |`binary`|`x`|  
    |`varbinary`|`x`|  
    |`image` <sup>2</sup>|`I`[`mage`]|  
    |`datetime`|**d[ate]**|  
    |`smalldatetime`|`D`|  
    |`time`|`te`|  
    |`date`|`de`|  
    |`datetime2`|`d2`|  
    |`datetimeoffset`|`do`|  
    |`decimal`|`n`|  
    |`numeric`|`n`|  
    |`float`|**f[loat]**|  
    |`real`|`r`|  
    |`Int`|**i[nt]**|  
    |`bigint`|`B[igint]`|  
    |`smallint`|**s[mallint]**|  
    |`tinyint`|**t[inyint]**|  
    |`money`|**m[oney]**|  
    |`smallmoney`|`M`|  
    |`bit`|`b[it]`|  
    |`uniqueidentifier`|`u`|  
    |`sql_variant`|`V[ariant]`|  
    |`timestamp`|`x`|  
    |`UDT` (um tipo de dados definido pelo usuário)|`U`|  
    |`XML`|`X`|  
  
     <sup>1</sup> a interação do tamanho do campo, do comprimento do prefixo e dos terminadores determina a quantidade de espaço de armazenamento alocada em um arquivo de dados para dados não caracteres que `char` são exportados como o tipo de armazenamento de arquivo.  
  
     <sup>2</sup> os `ntext`tipos `text`de dados `image` , e serão removidos em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No novo projeto de desenvolvimento, evite usar esses tipos de dados e planeje modificar os aplicativos que atualmente os utilizam. Use `nvarchar(max)`, `varchar(max)`e `varbinary(max)` em vez disso.  
  
## <a name="native-file-storage-types"></a>Tipos de armazenamento de arquivos nativos  
 Cada tipo de armazenamento de arquivo nativo é registrado no arquivo de formato como um tipo de dados do arquivo host correspondente.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|  
|-----------------------|-------------------------|  
|`char`<sup>1</sup>|SQLCHAR|  
|`varchar`|SQLCHAR|  
|`nchar`|SQLNCHAR|  
|`nvarchar`|SQLNCHAR|  
|`text` <sup>2</sup>|SQLCHAR|  
|`ntext` <sup>2</sup>|SQLNCHAR|  
|`binary`|SQLBINARY|  
|`varbinary`|SQLBINARY|  
|`image` <sup>2</sup>|SQLBINARY|  
|`datetime`|SQLDATETIME|  
|`smalldatetime`|SQLDATETIM4|  
|`decimal`|SQLDECIMAL|  
|`numeric`|SQLNUMERIC|  
|`float`|SQLFLT8|  
|`real`|SQLFLT4|  
|`int`|SQLINT|  
|`bigint`|SQLBIGINT|  
|`smallint`|SQLSMALLINT|  
|`tinyint`|SQLTINYINT|  
|`money`|SQLMONEY|  
|`smallmoney`|SQLMONEY4|  
|`bit`|SQLBIT|  
|`uniqueidentifier`|SQLUNIQUEID|  
|`sql_variant`|SQLVARIANT|  
|`timestamp`|SQLBINARY|  
|UDT (um tipo de dados definido pelo usuário)|SQLUDT|  
  
 <sup>1</sup> arquivos de dados que são armazenados em formato de `char` caractere usam como o tipo de armazenamento de arquivo. Então, para arquivos de dados de caractere, SQLCHAR é o único tipo de dados que aparece em um arquivo de formato.  
  
 <sup>2</sup> você não pode importar dados em `text`massa `ntext`para as `image` colunas, e que têm valores padrão.  
  
## <a name="additional-considerations-for-file-storage-types"></a>Considerações adicionais para tipos de armazenamento de arquivo  
 Quando você agrupa dados exportados de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados:  
  
-   Você sempre pode especificar `char` como o tipo de armazenamento de arquivo.  
  
-   Se você inserir um tipo de armazenamento de arquivo que representa uma conversão implícita inválida, o **bcp** falhará; por exemplo, embora você possa especificar `int` para `smallint` dados, se você especificar `smallint` for `int` data, resultado de estouro de erros.  
  
-   Quando tipos de dados que não são de caractere, como `float`, `money`, `datetime` ou `int`, são armazenados como seus tipos de bancos de dados, os dados são gravados para o arquivo de dados no formato nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  Depois que você especificar interativamente todos os campos em um comando **bcp**, o comando solicitará que salve suas respostas para cada campo em um arquivo de formato não XML. Para obter mais informações sobre arquivos de formato não XML, veja [Arquivos de formato não XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Especificar tamanho do campo usando bcp &#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)   
 [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [Especificar o tamanho de prefixo em arquivos de dados usando bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
