---
title: Especificar terminadores de campo e linha (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], terminators
- field terminators [SQL Server]
- data formats [SQL Server], terminators
- row terminators [SQL Server]
- terminators [SQL Server]
ms.assetid: f68b6782-f386-4947-93c4-e89110800704
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 42c2ee3fe98d6c6fc35d2417469bc3eec9fddd8c
ms.lasthandoff: 04/11/2017

---
# <a name="specify-field-and-row-terminators-sql-server"></a>Especificar terminadores de campo e linha (SQL Server)
  Para campos de dados de caracteres, caracteres de terminação opcionais permitem marcar o término de cada campo em um arquivo de dados com um *terminador de campo* e o término de cada linha com um *terminador de linha*. Os caracteres terminadores são um modo de indicar aos programas que leem o arquivo de dados onde um campo ou uma linha termina, e onde outro campo ou outra linha começa.  
  
> [!IMPORTANT]  
>  Quando você usa formato nativo ou nativo Unicode, usa prefixos de comprimento em vez de terminadores de campo. Dados de formato nativo podem conflituar com terminadores, pois um arquivo de dados de formato nativo é armazenado no formato de dados binário interno do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="characters-supported-as-terminators"></a>Caracteres que têm suporte como terminadores  
 O comando **bcp** , a instrução BULK INSERT e o provedor de conjunto de linhas em massa OPENROWSET oferecem suporte a uma variedade de caracteres como terminadores de campo ou de linha e sempre procura a primeira instância de cada terminador. A tabela a seguir lista os caracteres que têm suporte para terminadores.  
  
|Caractere terminador|Indicado por|  
|---------------------------|------------------|  
|Tab|\t<br /><br /> Esse é o terminador de campo padrão.|  
|Caractere de nova linha|\n<br /><br /> Esse é o terminador de linha padrão.|  
|Retorno de carro/avanço de linha|\r|  
|Barra invertida*|\\\|  
|Terminador nulo (terminador invisível)**|\0|  
|Qualquer caractere imprimível (caracteres de controle não são imprimíveis, exceto nulo, tabulação, nova linha e retorno de carro)|(*, A, t, l, etc.)|  
|Cadeia de caracteres de até 10 caracteres imprimíveis, incluindo alguns ou todos os terminadores listados anteriormente|(**\t\*\*, end, !!!!!!!!!!, \t—\n e assim por diante)|  
  
 *Somente os caracteres t, n, r, 0 e '\0' funcionam com o caractere de escape de barra invertida para produzir um caractere de controle.  
  
 **Embora o caractere de controle nulo (\0) não seja visível quando impresso, é um caractere distinto no arquivo de dados. Isso significa que usar o caractere de controle nulo como um terminador de campo ou de linha é diferente de não ter nenhum terminador de campo ou de linha.  
  
> [!IMPORTANT]  
>  Se um caractere terminador ocorrer dentro dos dados, ele será interpretado como um terminador, não como dados, e os dados depois daquele caractere serão interpretados como sendo parte do próximo campo ou registro. Portanto, escolha seus terminadores cuidadosamente para ter certeza de que eles nunca aparecerão em seus dados. Por exemplo, um terminador de campo de alternativo baixo não seria uma boa escolha para um terminador de campo se os dados contiverem esse alternativo baixo.  
  
## <a name="using-row-terminators"></a>Usando terminadores de linha  
 O terminador de linha pode ser o mesmo caractere que o terminador do último campo. Porém, geralmente um terminador de linha distinto é útil. Por exemplo, para produzir saída tabular, termine o último campo de cada linha com o caractere de nova linha (\n) e todos os outros campos com o caractere de tabulação (\t). Para colocar cada registro de dados em sua própria linha no arquivo de dados, especifique a combinação \r\n como terminador de linha.  
  
> [!NOTE]  
>  Quando você usa **bcp** de forma interativa e especifica \n (nova linha) como terminador de linha, o **bcp** automaticamente o prefixa com um caractere \r (retorno de carro), o que resulta em um terminador de linha \r\n.  
  
## <a name="specifying-terminators-for-bulk-export"></a>Especificando terminadores para exportação em massa  
 Quando você exporta em massa dados **char** ou **nchar** , e deseja usar um terminador não padrão, é necessário especificar o terminador para o comando **bcp** . Você pode especificar terminadores em qualquer uma das seguintes formas:  
  
-   Com um arquivo de formato que especifica o terminador campo por campo.  
  
    > [!NOTE]  
    >  Para obter informações sobre como usar arquivos de formato, veja [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
-   Sem um arquivo de formato, existem as seguintes alternativas:  
  
    -   Usar a opção **-t** para especificar o terminador de campo para todos os campos, exceto para o último campo na linha, e usar a opção **-r** para especificar um terminador de linha.  
  
    -   Usar uma opção de formato de caractere (**-c** ou **-w**) sem a opção **-t** , o que define o terminador de campo como o caractere de tabulação, \t. Isso é o mesmo que especificar **-t**\t.  
  
        > [!NOTE]  
        >  Se você especificar a opção **-n** (dados nativos) ou **-N** (dados nativos Unicode), os terminadores não serão inseridos.  
  
    -   Se um comando interativo **bcp** contiver a opção **in** ou **out** sem a opção de arquivo de formato (**-f**) ou uma opção de formato de dados (**-n**, **-c**, **-w**ou **-N**) e você tiver escolhido não identificar os tamanhos de prefixo e de campo, o comando solicitará o terminador de campo de cada campo com um padrão nenhum:  
  
         `Enter field terminator [none]:`  
  
         Geralmente, o padrão é uma escolha adequada. No entanto, para campos de dados **char** ou **nchar** , consulte a seguinte subseção, "Diretrizes para uso de terminadores". Para obter um exemplo que mostra esse prompt no contexto, veja [Especificar formatos de dados para compatibilidade usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
        > [!NOTE]  
        >  Depois que você especificar interativamente todos os campos em um comando **bcp**, o comando solicitará que salve suas respostas para cada campo em um arquivo de formato não XML. Para obter mais informações sobre arquivos de formato não XML, veja [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
### <a name="guidelines-for-using-terminators"></a>Diretrizes para uso de terminadores  
 Em algumas situações, um terminador é útil para um campo de dados **char** ou **nchar** . Por exemplo:  
  
-   Para uma coluna de dados que contém um valor nulo em um arquivo de dados que será importado em um programa que não entende as informações de comprimento de prefixo.  
  
     Qualquer coluna de dados que contenha um valor nulo é considerada de comprimento variável. Na ausência de comprimentos de prefixos, um terminador é necessário para identificar o término de um campo nulo, com a certeza de que os dados são corretamente interpretados.  
  
-   Para uma coluna longa de comprimento fixo cujo espaço é apenas parcialmente usado por várias linhas.  
  
     Nessa situação, especificar um terminador pode minimizar o espaço de armazenamento, permitindo que o campo seja tratado como um campo de comprimento variável.  
  
### <a name="examples"></a>Exemplos  
 Este exemplo exporta os dados em massa da tabela `AdventureWorks.HumanResources.Department` para o arquivo de dados `Department-c-t.txt` usando o formato de caractere, com uma vírgula como terminador de campo e o caractere de nova linha (\n) como terminador de linha.  
  
 O comando **bcp** contém as opções a seguir.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**-c**|Especifica que os campos de dados sejam carregados como dados de caracteres.|  
|**-t** `,`|Especifica uma vírgula (,) como terminador de campo.|  
|**-r** \n|Especifica o terminador de linha como um caractere de nova linha. Esse é o terminador de linha padrão, portanto especificá-lo é opcional.|  
|**-T**|Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para que o logon tenha êxito.|  
  
 Para obter mais informações, consulte [bcp Utility](../../tools/bcp-utility.md).  
  
 No prompt de comando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, digite:  
  
```  
bcp AdventureWorks.HumanResources.Department out C:\myDepartment-c-t.txt -c -t, -r \n -T  
```  
  
 Isso cria `Department-c-t.txt`que contém 16 registros com quatro campos cada. Os campos estão separados por uma vírgula.  
  
## <a name="specifying-terminators-for-bulk-import"></a>Especificando terminadores para importação em massa  
 Quando você importa em massa dados **char** ou **nchar** , o comando de importação em massa deve reconhecer os terminadores usados no arquivo de dados. A especificação dos terminadores depende do comando de importação em massa, como segue:  
  
-   **bcp**  
  
     A especificação de terminadores para uma operação de importação usa a mesma sintaxe que uma operação de exportação. Para obter mais informações, consulte "Especificando terminadores para exportação em massa", anteriormente neste tópico.  
  
-   BULK INSERT  
  
     Os terminadores podem ser especificados para campos individuais em um arquivo de formato ou para o arquivo de dados inteiro usando os qualificadores mostrados na tabela a seguir.  
  
    |Qualificador|Descrição|  
    |---------------|-----------------|  
    |FIELDTERMINATOR **='***field_terminator***'**|Especifica o terminador de campo a ser usado em arquivos de dados de caracteres e caracteres Unicode.<br /><br /> O padrão é \t (caractere de tabulação).|  
    |ROWTERMINATOR **='***row_terminator***'**|Especifica o terminador de linha a ser usado em arquivos de dados de caracteres e caracteres Unicode.<br /><br /> O padrão é \n (caractere de nova linha).|  
  
     Para obter mais informações, veja [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
-   INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
     Para o provedor de conjunto de linhas em massa OPENROWSET, podem ser especificados terminadores somente no arquivo de formato (que é necessário, exceto para tipos de dados de objeto grande). Se um arquivo de dados de caracteres usar um terminador não padrão, ele deverá ser definido no arquivo de formato. Para obter mais informações, veja [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md) e [Usar um arquivo de formato para importação de dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  
  
     Para obter mais informações sobre a cláusula OPENROWSET BULK, veja [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
### <a name="examples"></a>Exemplos  
 Os exemplos nesta seção importam em massa dados de caracteres do arquivo de dados `Department-c-t.txt` criado no exemplo anterior na tabela `myDepartment` no banco de dados de exemplo [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] . Antes de executar os exemplos, é necessário criar essa tabela. Para criar essa tabela no esquema **dbo** , no Editor de Consultas [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , execute o seguinte código:  
  
```tsql  
USE AdventureWorks;  
GO  
DROP TABLE myDepartment;  
CREATE TABLE myDepartment   
(DepartmentID smallint,  
Name nvarchar(50),  
GroupName nvarchar(50) NULL,  
ModifiedDate datetime not NULL CONSTRAINT DF_AddressType_ModifiedDate DEFAULT (GETDATE())  
);  
GO 
```  
  
#### <a name="a-using-bcp-to-interactively-specify-terminators"></a>A. Usando bcp para especificar terminadores interativamente  
 O exemplo a seguir importa em massa o arquivo de dados `Department-c-t.txt` usando um comando `bcp` . Esse comando usa as mesmas opções de comando que o comando de exportação em massa. Para obter mais informações, consulte "Especificando terminadores para exportação em massa", anteriormente neste tópico.  
  
 No prompt de comando do Windows, insira:  
  
```  
bcp AdventureWorks..myDepartment in C:\myDepartment-c-t.txt -c -t , -r \n -T  
```  
  
#### <a name="b-using-bulk-insert-to-interactively-specify-terminators"></a>B. Usando BULK INSERT para especificar terminadores interativamente  
 O exemplo a seguir importa em massa o arquivo de dados `Department-c-t.txt` usando uma instrução `BULK INSERT` que usa os qualificadores mostrados na tabela a seguir.  
  
|Opção|Atributo|  
|------------|---------------|  
|DATAFILETYPE **='**char**'**|Especifica que os campos de dados sejam carregados como dados de caracteres.|  
|FIELDTERMINATOR **='**`,`**'**|Especifica uma vírgula (`,`) como terminador de campo.|  
|ROWTERMINATOR **='**`\n`**'**|Especifica o terminador de linha como um caractere de nova linha.|  
  
 No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , execute o seguinte código:  
  
```tsql  
USE AdventureWorks;  
GO  
BULK INSERT myDepartment FROM 'C:\myDepartment-c-t.txt'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      ROWTERMINATOR = '\n'  
);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Especificar tamanho do campo usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)   
 [Especificar o tamanho de prefixo em arquivos de dados usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [Especificar tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  

