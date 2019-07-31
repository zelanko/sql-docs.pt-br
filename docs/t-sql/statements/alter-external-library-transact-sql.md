---
title: ALTER EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
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
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: 461a9c27b456f3f3955d5bcb7229e0c4448a0996
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471141"
---
# <a name="alter-external-library-transact-sql"></a>ALTER EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Modifica o conteúdo de uma biblioteca de pacotes externa existente.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
> [!NOTE]
> No SQL Server 2017, há compatibilidade apenas com a linguagem R e a plataforma Windows. Há suporte para as linguagens R, Python e externas nas plataformas Windows e Linux no SQL Server 2019 CTP 2.4 e posterior.
::: moniker-end

::: moniker range="=azuresqldb-current"
> [!NOTE]
> No Banco de Dados SQL do Azure, você pode alterar uma biblioteca removendo-a e, em seguida, usando **sqlmlutils** para instalar a versão alterada. Para obter mais informações sobre **sqlmlutils**, confira [Adicionar um pacote com sqlmlutils](/azure/sql-database/sql-database-machine-learning-services-add-r-packages#add-a-package-with-sqlmlutils).
::: moniker-end

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
    [, PLATFORM = <platform> )
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

<platform> :: = 
{
      WINDOWS
    | LINUX
}

<language> :: = 
{
      'R'
    | 'Python'
    | <external_language>
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

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
## <a name="syntax-for-azure-sql-database"></a>Sintaxe do Banco de Dados SQL do Azure

```text
CREATE EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
    (CONTENT = <library_bits>)  
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

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**file_spec**

Especifica o conteúdo do pacote para uma plataforma específica. Há compatibilidade apenas com um artefato de arquivo por plataforma.

O arquivo pode ser especificado na forma de um caminho local ou de um caminho de rede. Se a opção de fonte de dados for especificada, o nome do arquivo poderá ser um caminho relativo em relação ao contêiner referenciado em `EXTERNAL DATA SOURCE`.

Opcionalmente, uma plataforma de sistema operacional para o arquivo pode ser especificada. Somente um artefato ou conteúdo de arquivo é permitido para cada plataforma de sistema operacional em uma linguagem ou um tempo de execução específico.

::: moniker-end

**library_bits**

Especifica o conteúdo do pacote como um literal hexadecimal, semelhante aos assemblies.

Essa opção será útil se você tiver a permissão necessária para alterar uma biblioteca, mas o acesso a arquivos no servidor estiver restrito e não for possível salvar o conteúdo em um caminho que o servidor possa acessar.

Nesse caso, você pode passar o conteúdo do pacote como uma variável em formato binário.

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**PLATFORM = WINDOWS**

Especifica a plataforma para o conteúdo da biblioteca. Esse valor é necessário ao modificar uma biblioteca existente para adicionar uma plataforma diferente.
No SQL Server 2017, o Windows é a única plataforma compatível.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**PLATAFORMA**

Especifica a plataforma para o conteúdo da biblioteca. Esse valor é necessário ao modificar uma biblioteca existente para adicionar uma plataforma diferente. 
No SQL Server 2019, o Windows e o Linux são as plataformas compatíveis.
::: moniker-end

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**LANGUAGE = 'R'**

Especifica a linguagem do pacote. O R tem suporte no SQL Server 2017.
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
**LANGUAGE = 'R'**

Especifica a linguagem do pacote. O R tem suporte no Banco de Dados SQL do Azure.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**language**

Especifica a linguagem do pacote. O valor pode ser **R**, **Python** ou o nome de uma linguagem externa (confira [CREATE EXTERNAL LANGUAGE](create-external-language-transact-sql.md)).
::: moniker-end

## <a name="remarks"></a>Remarks

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
Para a linguagem R, os pacotes precisam ser preparados no formato de arquivos compactados com a extensão .ZIP para Windows. No SQL Server 2017, apenas a plataforma Windows é compatível.  
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para a linguagem R, ao usar um arquivo, os pacotes precisam ser preparados no formato de arquivos mortos compactados com a extensão .zip. 

Para a linguagem Python, o pacote em um arquivo .whl ou .zip deve estar preparado na forma de um arquivo morto compactado. Se o pacote já for um arquivo .zip, ele deverá ser incluído em um novo arquivo .zip. Carregar um pacote diretamente como arquivo .whl ou .zip não é uma ação compatível atualmente.
::: moniker-end

A instrução `ALTER EXTERNAL LIBRARY` carrega apenas os bits de biblioteca para o banco de dados. A biblioteca modificada é instalada quando um usuário executa o código no [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) que chama a biblioteca.

## <a name="permissions"></a>Permissões

Por padrão, os usuários do **dbo** ou membros da função **db_owner** têm permissão para executar ALTER EXTERNAL LIBRARY. Além disso, os usuários que criaram a biblioteca externa podem alterá-la.

## <a name="examples"></a>Exemplos

Os exemplos a seguir alteram uma biblioteca externa chamada `customPackage`.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
### <a name="replace-the-contents-of-a-library-using-a-file"></a>Substituir o conteúdo de uma biblioteca usando um arquivo

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
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para a linguagem Python no SQL Server 2019, o exemplo também funciona, substituindo `'R'` com `'Python'`.
::: moniker-end

### <a name="alter-an-existing-library-using-a-byte-stream"></a>Alterar uma biblioteca existente usando um fluxo de bytes

O exemplo a seguir altera a biblioteca existente, passando os novos bits como um literal hexadecimal.

```SQL
ALTER EXTERNAL LIBRARY customLibrary 
SET (CONTENT = 0xABC123...) WITH (LANGUAGE = 'R');
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
