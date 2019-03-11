---
title: ALTER EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc590bb618f9a95a0fbe7b0a9c173a64698cdf1e
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017962"
---
# <a name="alter-external-library-transact-sql"></a>ALTER EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Modifica o conteúdo de uma biblioteca de pacotes externa existente.

> [!NOTE]
> No SQL Server 2017, há compatibilidade apenas com a linguagem R e a plataforma Windows. R, Python e Java na plataforma do Windows são compatíveis com o SQL Server 2019 CTP 2.3. O suporte a Python e Linux está previsto para uma versão posterior.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2019"></a>Sintaxe do SQL Server 2019

```text
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = <language> )
[ ; ]

<file_spec> ::=
{
    (CONTENT = { <client_library_specifier> | <library_bits> | NONE}
    [, PLATFORM = WINDOWS )
}

<client_library_specifier> :: =
{
      '[\\computer_name\]share_name\[path\]manifest_file_name'
    | '[local_path\]manifest_file_name'
    | '<relative_path_in_external_data_source>'
}

<library_bits> :: =
{ 
      varbinary_literal 
    | varbinary_expression 
}

<language> :: = 
{
      'R'
    | 'Python'
    | 'Java'
}
```
::: moniker-end
::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2017"></a>Sintaxe do SQL Server 2017

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
{
      '[\\computer_name\]share_name\[path\]manifest_file_name'
    | '[local_path\]manifest_file_name'
    | '<relative_path_in_external_data_source>'
}

<library_bits> :: =
{ 
      varbinary_literal 
    | varbinary_expression 
}
```
::: moniker-end

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

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**language**

Especifica a linguagem do pacote. O valor pode ser **R**, **Python** ou **Java**.
::: moniker-end

## <a name="remarks"></a>Remarks

Para a linguagem R, os pacotes precisam ser preparados no formato de arquivos compactados com a extensão .ZIP para Windows. Atualmente, há compatibilidade apenas com a plataforma Windows.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para a linguagem Python, o pacote em um arquivo .whl ou .zip deve estar preparado na forma de um arquivo morto compactado. Se o pacote já for um arquivo .zip, ele deverá ser incluído em um novo arquivo .zip. Carregar um pacote diretamente como arquivo .whl ou .zip não é uma ação compatível atualmente.
::: moniker-end

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

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para a linguagem Python no SQL Server 2019, o exemplo também funciona, substituindo `'R'` com `'Python'`.
::: moniker-end
### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>b. Alterar uma biblioteca existente usando um fluxo de bytes

O exemplo a seguir altera a biblioteca existente, passando os novos bits como um literal hexadecimal.

```SQL
ALTER EXTERNAL LIBRARY customLibrary 
SET (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para a linguagem Python no SQL Server 2019, o exemplo também funciona, substituindo `'R'` com `'Python'`.
::: moniker-end

> [!NOTE]
> Este exemplo de código demonstra apenas a sintaxe; o valor binário em `CONTENT =` foi truncado para facilitar a leitura e não cria uma biblioteca de trabalho. O conteúdo real da variável binária deveria ser maior.

## <a name="see-also"></a>Confira também

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md) 
