---
title: ALTER biblioteca externa (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 541419770828e01cca82fb33ead1b22170f8e4f3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-external-library-transact-sql"></a>ALTER biblioteca externa (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

Modifica o conteúdo da biblioteca existente.  

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

**PLATAFORMA = WINDOWS**

Especifica a plataforma para o conteúdo da biblioteca. Esse valor é necessário ao modificar uma biblioteca existente para adicionar uma plataforma diferente. Windows é a única plataforma com suporte.

## <a name="remarks"></a>Comentários

Para a linguagem R, os pacotes devem ser preparados na forma de arquivos compactados com o. Extensão ZIP para Windows. Atualmente, apenas a plataforma do Windows tem suporte.  
O `ALTER EXTERNAL LIBRARY` instrução carrega apenas os bits de biblioteca para o banco de dados. A biblioteca modificada, na verdade, não está instalada até que um usuário executa um script externo posteriormente, executando [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="permissions"></a>Permissões
Requer o `ALTER ANY EXTERNAL LIBRARY` permissão. Os usuários que criou uma biblioteca externa, é possível alterar essa biblioteca externa.

## <a name="examples"></a>Exemplos

O exemplo a seguir modifica uma biblioteca externa chamada customPackage.

```sql  
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  
Em seguida, execute o `sp_execute_external_script` procedimento, para instalar a biblioteca.

```sql   
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)

# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
with result sets (([result] int));    
```


## <a name="see-also"></a>Consulte também  
[Criar biblioteca externa (Transact-SQL)](create-external-library-transact-sql.md)
[DROP biblioteca externa (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

