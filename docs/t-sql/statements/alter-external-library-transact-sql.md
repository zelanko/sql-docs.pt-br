---
title: ALTER EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/05/2018
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
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: e2fb628e2f832b7d1b73a2e3fefae1fb1d6b8e2b
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="alter-external-library-transact-sql"></a>ALTER EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Modifica o conteúdo de uma biblioteca de pacotes externa existente.

## <a name="syntax"></a>Sintaxe

```text
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

**library_name**

Especifica o nome de uma biblioteca de pacotes existente. As bibliotecas estão no escopo do usuário. Os nomes de bibliotecas devem ser exclusivos no contexto de um usuário ou proprietário específico.

O nome da biblioteca não pode ser atribuído arbitrariamente. Ou seja, você precisa usar o nome que o tempo de execução de chamada espera ao carregar o pacote.

**owner_name**

Especifica o nome do usuário ou da função que é a proprietária da biblioteca externa.

**file_spec**

Especifica o conteúdo do pacote para uma plataforma específica. Há compatibilidade apenas com um artefato de arquivo por plataforma.

O arquivo pode ser especificado na forma de um caminho local ou de um caminho de rede. Se a opção de fonte de dados for especificada, o nome do arquivo poderá ser um caminho relativo em relação ao contêiner referenciado em `EXTERNAL DATA SOURCE`.

Opcionalmente, uma plataforma de sistema operacional para o arquivo pode ser especificada. Somente um artefato ou conteúdo de arquivo é permitido para cada plataforma de sistema operacional em uma linguagem ou um tempo de execução específico.

**library_bits**

Especifica o conteúdo do pacote como um literal hexadecimal, semelhante aos assemblies. 

Essa opção será útil se você tiver a permissão necessária para alterar uma biblioteca, mas o acesso a arquivos no servidor estiver restrito e não for possível salvar o conteúdo em um caminho que o servidor possa acessar.

Nesse caso, você pode passar o conteúdo do pacote como uma variável em formato binário.

**PLATFORM = WINDOWS**

Especifica a plataforma para o conteúdo da biblioteca. Esse valor é necessário ao modificar uma biblioteca existente para adicionar uma plataforma diferente. O Windows é a única plataforma com suporte.

## <a name="remarks"></a>Remarks

Para a linguagem R, os pacotes precisam ser preparados no formato de arquivos compactados com a extensão .ZIP para Windows. Atualmente, há compatibilidade apenas com a plataforma Windows.  

A instrução `ALTER EXTERNAL LIBRARY` carrega apenas os bits de biblioteca para o banco de dados. A biblioteca modificada é instalada quando um usuário executa o código no [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) que chama a biblioteca.

## <a name="permissions"></a>Permissões

Por padrão, os usuários do **dbo** ou membros da função **db_owner** têm permissão para executar ALTER EXTERNAL LIBRARY. Além disso, os usuários que criaram a biblioteca externa podem alterá-la.

## <a name="examples"></a>Exemplos

Os exemplos a seguir alteram uma biblioteca externa chamada `customPackage`.

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. Substituir o conteúdo de uma biblioteca usando um arquivo

O exemplo a seguir modifica uma biblioteca externa chamada `customPackage`, usando um arquivo compactado que contém os bits atualizados.

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
@script=N'library(customPackage)'
;
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. Alterar uma biblioteca existente usando um fluxo de bytes

O exemplo a seguir altera a biblioteca existente, passando os novos bits como um literal hexadecimal.

```SQL
ALTER EXTERNAL LIBRARY customLibrary 
SET (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

> [!NOTE]
> Este exemplo de código demonstra apenas a sintaxe; o valor binário em `CONTENT =` foi truncado para facilitar a leitura e não cria uma biblioteca de trabalho. O conteúdo real da variável binária deveria ser maior.

## <a name="see-also"></a>Consulte também

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md) 
