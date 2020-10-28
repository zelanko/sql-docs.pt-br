---
description: ALTER EXTERNAL LANGUAGE (Transact-SQL) – SQL Server
title: ALTER EXTERNAL LANGUAGE (Transact-SQL) – SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 006a0577292ba825a3d28cd63cc573ac35cc5771
ms.sourcegitcommit: bd3a135f061e4a49183bbebc7add41ab11872bae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92300430"
---
# <a name="alter-external-language-transact-sql"></a>ALTER EXTERNAL LANGUAGE (Transact-SQL)
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Modifica o conteúdo em uma extensão de linguagem externa existente no banco de dados.

## <a name="syntax"></a>Sintaxe

```syntaxsql
ALTER EXTERNAL LANGUAGE language_name  
[ AUTHORIZATION owner_name ]
{
    SET <file_spec>
    | ADD <file_spec>
    | REMOVE <file_spec>
}
[ ; ]  

<file_spec> ::=  
{
    ( CONTENT = {<external_lang_specifier> | <content_bits>,
    FILE_NAME = <external_lang_file_name>
    [, PLATFORM = <platform> ]
    [, PARAMETERS = <external_lang_parameters> ]
    [, ENVIRONMENT_VARIABLES = <external_lang_env_variables> ] )
}

<external_lang_specifier> :: =  
{
    '[file_path\]os_file_name'  
}

<content_bits> :: =  
{
    varbinary_literal
   | varbinary_expression
}

<external_lang_file_name> :: =  
'extension_file_name'

<platform> :: =
{
   WINDOWS
  | LINUX
}

< external_lang_parameters > :: =  
'extension_specific_parameters'
```

### <a name="arguments"></a>Argumentos

**language_name**

As linguagens são objetos no escopo do banco de dados. Os nomes das linguagens precisam ser exclusivos no banco de dados.

**owner_name**

Especifica o nome da função ou do usuário que é o proprietário da linguagem externa. Se não estiver especificada, a propriedade será dada ao usuário atual. Dependendo das permissões, outros usuários podem precisar receber a permissão explícita para executar scripts usando uma linguagem específica.

**file_spec**

Especifica o conteúdo da extensão de linguagem. Apenas um filespec é permitido para uma linguagem específica, por plataforma. 

**external_lang_specifier**

O caminho de arquivo completo para o arquivo .zip ou tar.gz que contém o código de extensões. Esse conteúdo pode ser um caminho para um arquivo .zip (no Windows) ou tar.gz (no Linux).

**content_bits**

Especifica o conteúdo da linguagem como um literal hexadecimal, de forma semelhante aos assemblies.
Essa opção será útil se você precisar criar uma linguagem ou alterar uma linguagem existente (e tiver as permissões necessárias para fazer isso), mas o sistema de arquivos no servidor for restrito e você não puder copiar os arquivos de biblioteca para uma localização que o servidor possa acessar.

**external_lang_file_name**

Nome do arquivo de extensão .dll ou .so. Isso é necessário para identificar o arquivo correto, nos casos em que há vários arquivos .dll ou .so no <external_lang_specifier> .zip ou tar.gz.

**external_lang_parameters**

Isso fornece uma possibilidade de fornecer um conjunto de parâmetros para o runtime de linguagem externa. Os valores de parâmetro são fornecidos para o runtime externo após o início do processo externo. No entanto, as variáveis de ambiente são acessíveis para a extensão de linguagem antes da inicialização do processo externo.

**external_lang_env_variables**

Isso permite uma possibilidade de fornecer um conjunto de variáveis de ambiente ao runtime da linguagem externa antes da inicialização do processo externo. Um exemplo de uma variável de ambiente é, por exemplo, o diretório base do próprio runtime. Por exemplo:  JRE_HOME.

**platform**

Esse parâmetro é necessário para cenários de sistema operacional híbrido. Em uma arquitetura híbrida, a linguagem precisa ser registrada uma vez por plataforma. O nome da plataforma e da linguagem será a chave exclusiva por linguagem externa. Se nenhuma plataforma for especificada, o sistema operacional atual será considerado.

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários

Atualmente, não há suporte para **PARAMETERS** e **ENVIRONMENT_VARIABLES** .

## <a name="permissions"></a>Permissões

Requer a permissão `ALTER ANY EXTERNAL LANGUAGE`. Por padrão, os usuários que têm o **dbo** que seja membro da função **db_owner** têm permissões para alterar uma linguagem externa. Para todos os outros usuários, é necessário conceder permissão a eles explicitamente com uma instrução [GRANT](./grant-database-permissions-transact-sql.md), especificando ALTER ANY EXTERNAL LANGUAGE como o privilégio.

## <a name="examples"></a>Exemplos

### <a name="alter-an-external-language-in-a-database"></a>Alterar uma linguagem externa em um banco de dados  

O exemplo a seguir adiciona uma linguagem externa chamada Java a um banco de dados no SQL Server no Windows.

```sql
ALTER EXTERNAL LANGUAGE Java 
SET (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

## <a name="see-also"></a>Confira também

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[DROP EXTERNAL LANGUAGE (Transact-SQL)](drop-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)