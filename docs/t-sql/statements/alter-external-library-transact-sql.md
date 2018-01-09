---
title: ALTER biblioteca externa (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: e679664f02ffcb08d811a66229a21f1bdaf08077
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="alter-external-library-transact-sql"></a>ALTER biblioteca externa (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Modifica o conteúdo de uma biblioteca existente do pacote externo.

## <a name="syntax"></a>Sintaxe

```
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = 'R' )
[ ; ]

<file_spec> ::=
{
(CONTENT = { <client_library_specifier> | <library_bits> | NONE}
[, PLATFORM = WINDOWS )
}

<client_library_specifier> :: =
  '[\\computer_name\]share_name\[path\]manifest_file_name'
| '[local_path\]manifest_file_name'
| '<relative_path_in_external_data_source>'

<library_bits> :: =
{ varbinary_literal | varbinary_expression }
```

### <a name="arguments"></a>Argumentos

**nome_da_biblioteca**

Especifica o nome de uma biblioteca de pacote existente. Bibliotecas de escopo serão o usuário. Ou seja, nomes de biblioteca são considerados exclusivos dentro do contexto de um usuário específico ou um proprietário.

**owner_name**

Especifica o nome do usuário ou função que possui a biblioteca externa.

**file_spec**

Especifica o conteúdo do pacote para uma plataforma específica. Há suporte para o artefato de apenas um arquivo por plataforma.

O arquivo pode ser especificado na forma de um caminho local ou um caminho de rede. Se a opção de fonte de dados for especificada, o nome do arquivo pode ser um caminho relativo em relação ao contêiner referenciado no `EXTERNAL DATA SOURCE`.

Opcionalmente, uma plataforma de sistema operacional para o arquivo pode ser especificada. O artefato de apenas um arquivo ou o conteúdo é permitido para cada plataforma de sistema operacional para um idioma específico ou o tempo de execução.

**DATA_SOURCE = external_data_source_name**

Especifica o nome da fonte de dados externa que contém o local do arquivo de biblioteca. Esse local deve fazer referência a um caminho de armazenamento de BLOBs do Azure. Para criar uma fonte de dados externa, use [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](create-external-data-source-transact-sql.md).

> [!IMPORTANT] 
> Atualmente, os blobs não têm suporte como uma fonte de dados na versão SQL Server 2017.

**library_bits**

Especifica o conteúdo do pacote como um literal hexadecimal, semelhante aos assemblies. Esta opção permite aos usuários criar uma biblioteca para alterar a biblioteca se tem a permissão necessária, mas não tem acesso ao caminho do arquivo para qualquer pasta que o servidor possa acessar.

**PLATAFORMA = WINDOWS**

Especifica a plataforma para o conteúdo da biblioteca. Esse valor é necessário ao modificar uma biblioteca existente para adicionar uma plataforma diferente. Windows é a única plataforma com suporte.

## <a name="remarks"></a>Remarks

Para a linguagem R, os pacotes devem ser preparados na forma de arquivos compactados com o. Extensão ZIP para Windows. Atualmente, apenas a plataforma do Windows tem suporte.  

O `ALTER EXTERNAL LIBRARY` instrução carrega apenas os bits de biblioteca para o banco de dados. A biblioteca modificada, na verdade, não está instalada até que um usuário executa um script externo posteriormente, executando [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="permissions"></a>Permissões

Requer o `ALTER ANY EXTERNAL LIBRARY` permissão. Os usuários que criou uma biblioteca externa, é possível alterar essa biblioteca externa.

## <a name="examples"></a>Exemplos

Os exemplos a seguir modifica uma biblioteca externa chamada customPackage.

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. Substitua o conteúdo de uma biblioteca usando um arquivo

O exemplo a seguir modifica uma biblioteca externa chamada customPackage, usando um arquivo compactado que contém os bits atualizados.

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

Para instalar a biblioteca atualizada, execute o procedimento armazenado `sp_execute_external_script`.

```sql   
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
WITH RESULT SETS (([result] int));
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. Alterar uma biblioteca existente usando um fluxo de bytes

O exemplo a seguir altera a biblioteca existente, passando os novos bits como um hexadecimal literal.

```SQL
ALTER EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

## <a name="see-also"></a>Consulte também  

[Criar biblioteca externa (Transact-SQL)](create-external-library-transact-sql.md)
[DROP biblioteca externa (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
