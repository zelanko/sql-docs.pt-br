---
description: CREATE EXTERNAL LANGUAGE (Transact-SQL) – SQL Server
title: CREATE EXTERNAL LANGUAGE (Transact-SQL) – SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.technology: language-extensions
ms.topic: language-reference
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6a32e4c18096aefc88342104ae54124d6e88cefa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426678"
---
# <a name="create-external-language-transact-sql"></a>CREATE EXTERNAL LANGUAGE (Transact-SQL)
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Registra as extensões de linguagem externa no banco de dados com base no fluxo de bytes ou no caminho de arquivo especificado. Essa instrução funciona como um mecanismo genérico para o administrador de banco de dados registrar novas extensões de linguagens externas em qualquer plataforma de sistema operacional compatível com o SQL Server. Para saber mais, confira [Extensões de Linguagem](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview).

> [!NOTE]
> No momento, apenas o **Java** é compatível como linguagem externa. **R** e **Python** são nomes reservados, e nenhuma linguagem externa pode ser criada com esses nomes específicos. Para saber mais sobre como usar **R** e **Python**, confira [Serviços de Machine Learning do SQL Server](https://docs.microsoft.com/sql/machine-learning/).

## <a name="syntax"></a>Sintaxe

```text
CREATE EXTERNAL LANGUAGE language_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
[ ; ]  

<file_spec> ::=  
{
    ( CONTENT = { <external_lang_specifier> | <content_bits> },
    FILE_NAME = <external_lang_file_name>
    [ , PLATFORM = <platform> ]
    [ , PARAMETERS = <external_lang_parameters> ]
    [ , ENVIRONMENT_VARIABLES = <external_lang_env_variables> ] )
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

<external_lang_parameters> :: =  
'extension_specific_parameters'
```

### <a name="arguments"></a>Argumentos

**language_name**

As linguagens são objetos no escopo do banco de dados. Os nomes das linguagens precisam ser exclusivos no banco de dados.

**owner_name**

Especifica o nome da função ou do usuário que é o proprietário da linguagem externa. Se não estiver especificada, a propriedade será dada ao usuário atual. Dependendo das permissões, outros usuários podem precisar receber a permissão explícita para executar scripts usando uma linguagem específica.

**file_spec**

Especifica o conteúdo da extensão da linguagem. Apenas um filespec é permitido para uma linguagem específica, por plataforma.

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

## <a name="permissions"></a>Permissões

Requer a permissão `CREATE EXTERNAL LANGUAGE`. Por padrão, os usuários que têm o **dbo** que seja membro da função **db_owner** têm permissões para criar uma linguagem externa. Para todos os outros usuários, é necessário conceder permissão a eles explicitamente com uma instrução [GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql), especificando CREATE EXTERNAL LANGUAGE como o privilégio.

Para modificar uma biblioteca, é necessário ter a permissão separada, `ALTER ANY EXTERNAL LANGUAGE`.

### <a name="execute-external-script-permission"></a>Permissão EXECUTE EXTERNAL SCRIPT

Você pode usar as permissões EXECUTE EXTERNAL SCRIPT, para que a execução do script externo possa ser concedida em linguagens específicas. Isso é diferente da permissão de banco de dados EXECUTE ANY EXTERNAL SCRIPT, que não permite a concessão da permissão de execução em uma linguagem específica.

Isso significa que os usuários não **dbo** precisam receber a permissão para executar uma linguagem específica:

```sql
GRANT EXECUTE EXTERNAL SCRIPT ON EXTERNAL LANGUAGE ::language_name 
TO database_principal_name;
```

### <a name="reference-permissions-to-external-libraries"></a>Permissões de referência para bibliotecas externas

De forma semelhante aos assemblies, as permissões de referência são necessárias para linguagens externas, de modo que haja um vínculo entre bibliotecas externas e linguagens externas. Por exemplo, se uma linguagem externa precisar ser removida, primeiro o usuário precisará garantir que todas as bibliotecas externas que referenciam essa linguagem sejam removidas. Você pode exibir a linguagem externa como um objeto de nível superior às bibliotecas externas em uma hierarquia.

## <a name="examples"></a>Exemplos

### <a name="a-create-an-external-language-in-a-database"></a>a. Criar uma linguagem externa em um banco de dados  

O exemplo a seguir adiciona uma linguagem externa chamada Java a um banco de dados no SQL Server no Windows.

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

### <a name="b-create-an-external-language-for-both-windows-and-linux"></a>B. Criar uma linguagem externa para o Windows e o Linux

Você pode especificar até dois `<file_spec>`, um para o Windows e outro para o Linux.

```sql
CREATE EXTERNAL LANGUAGE Java
FROM
(CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll', PLATFORM = WINDOWS),
(CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so', PLATFORM = LINUX);
GO
```
### <a name="c-grant-permissions-to-execute-external-script"></a>C. Conceder permissões para executar o script externo

O exemplo a seguir concede acesso de entidade de segurança **mylogin** para executar scripts usando a linguagem externa **Java**.

```sql
GRANT EXECUTE EXTERNAL SCRIPT ON EXTERNAL LANGUAGE ::Java 
TO mylogin;
```


## <a name="see-also"></a>Confira também

[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[DROP EXTERNAL LANGUAGE (Transact-SQL)](drop-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
