---
title: CREATE EXTERNAL LIBRARY (Transact-SQL) – SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 852b98c1ee0eecba21b426c74397985208fd2178
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67140796"
---
# <a name="create-external-library-transact-sql"></a>CREATE EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

Carrega os arquivos de pacotes do R, Python ou Java em um banco de dados do caminho de arquivo ou fluxo de bytes especificado. Essa instrução funciona como um mecanismo genérico para que o administrador de banco de dados carregue os artefatos necessários para novos tempos de execução de idiomas externos e plataformas de sistema operacional compatíveis com o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]. 

> [!NOTE]
> No SQL Server 2017, há compatibilidade apenas com a linguagem R e a plataforma Windows. Há suporte para as linguagens R, Python e externas nas plataformas Windows e Linux no SQL Server 2019 CTP 3.0.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2019"></a>Sintaxe do SQL Server 2019

```text
CREATE EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH ( LANGUAGE = <language> )  
[ ; ]  

<file_spec> ::=  
{  
    (CONTENT = { <client_library_specifier> | <library_bits> }  
    [, PLATFORM = <platform> ])  
}  

<client_library_specifier> :: = 
{
    '[file_path\]manifest_file_name'  
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
CREATE EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
    (CONTENT = { <client_library_specifier> | <library_bits> }  
    [, PLATFORM = WINDOWS ])  
}  

<client_library_specifier> :: = 
{
    '[file_path\]manifest_file_name'
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

As bibliotecas são adicionadas ao banco de dados no escopo do usuário. Os nomes de bibliotecas devem ser exclusivos no contexto de um usuário ou proprietário específico. Por exemplo, dois usuários **RUser1** e **RUser2** podem individual e separadamente carregar a biblioteca do R `ggplot2`. No entanto, se **RUser1** quiser carregar uma versão mais recente do `ggplot2`, a segunda instância deve ter um nome diferente ou deve substituir a biblioteca existente. 

Os nomes de biblioteca não podem ser atribuídos arbitrariamente; o nome da biblioteca deve ter o mesmo nome necessário para carregar a biblioteca no script externo.

**owner_name**

Especifica o nome do usuário ou da função que é a proprietária da biblioteca externa. Se não estiver especificada, a propriedade será dada ao usuário atual.

As bibliotecas que pertencem ao proprietário do banco de dados são consideradas globais para o banco de dados e o tempo de execução. Em outras palavras, os proprietários do banco de dados podem criar bibliotecas que contêm um conjunto comum de bibliotecas ou pacotes que são compartilhados por muitos usuários. Quando uma biblioteca externa é criada por um usuário diferente do usuário `dbo`, a biblioteca externa é particular somente a esse usuário.

Quando o usuário **RUser1** executa um script externo, o valor de `libPath` pode conter vários caminhos. O primeiro caminho é sempre o caminho para a biblioteca compartilhada criado pelo proprietário do banco de dados. A segunda parte de `libPath` especifica o caminho que contém os pacotes carregados individualmente por **RUser1**.

**file_spec**

Especifica o conteúdo do pacote para uma plataforma específica. Há compatibilidade apenas com um artefato de arquivo por plataforma.

O arquivo pode ser especificado no formato de um caminho local ou caminho de rede.

Ao tentar acessar o arquivo especificado em **<client_library_specifier>** , o SQL Server representa o contexto de segurança do logon atual do Windows. Se **<client_library_specifier>** especificar um local de rede (caminho UNC), a representação do logon atual não será repassada ao local de rede devido a limitações de delegação. Nesse caso, o acesso é feito usando o contexto de segurança da conta de serviço do SQL Server. Para obter mais informações, consulte [Credenciais (Mecanismo de Banco de Dados)](../../relational-databases/security/authentication-access/credentials-database-engine.md).

Opcionalmente, uma plataforma de sistema operacional para o arquivo pode ser especificada. Somente um artefato ou conteúdo de arquivo é permitido para cada plataforma de sistema operacional em uma linguagem ou um tempo de execução específico.

**library_bits**

Especifica o conteúdo do pacote como um literal hexadecimal, semelhante aos assemblies. 

Essa opção será útil se você precisar criar uma biblioteca ou alterar uma biblioteca existente (e tiver as permissões necessárias para fazer isso), mas o sistema de arquivos no servidor for restrito e você não puder copiar os arquivos de biblioteca para um local que o servidor possa acessar.

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**PLATFORM = WINDOWS**

Especifica a plataforma para o conteúdo da biblioteca. O valor usa como padrão a plataforma de host na qual o SQL Server está sendo executado. Portanto, o usuário não precisa especificar o valor. É necessário no caso em que várias plataformas são compatíveis ou quando o usuário precisa especificar outra plataforma. 

No SQL Server 2017, o Windows é a única plataforma compatível.
::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**PLATAFORMA**

Especifica a plataforma para o conteúdo da biblioteca. O valor usa como padrão a plataforma de host na qual o SQL Server está sendo executado. Portanto, o usuário não precisa especificar o valor. É necessário no caso em que várias plataformas são compatíveis ou quando o usuário precisa especificar outra plataforma.

No SQL Server 2019, o Windows e o Linux são as plataformas compatíveis.

**language**

Especifica a linguagem do pacote. O valor pode ser `R`, `Python` ou o nome de uma [linguagem externa criada](create-external-language-transact-sql.md).
::: moniker-end

## <a name="remarks"></a>Remarks

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
Para a linguagem R, ao usar um arquivo, os pacotes precisam ser preparados no formato de arquivos mortos compactados com a extensão .ZIP para o Windows. No SQL Server 2017, apenas a plataforma Windows é compatível.
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para a linguagem R, ao usar um arquivo, os pacotes precisam ser preparados no formato de arquivos mortos compactados com a extensão .zip.  

Para a linguagem Python, o pacote em um arquivo .whl ou .zip deve estar preparado na forma de um arquivo morto compactado. Se o pacote já for um arquivo .zip, ele deverá ser incluído em um novo arquivo .zip. Carregar um pacote diretamente como arquivo .whl ou .zip não é uma ação compatível atualmente.
::: moniker-end

A instrução `CREATE EXTERNAL LIBRARY` carrega os bits de biblioteca no banco de dados. A biblioteca é instalada quando um usuário executa um script externo usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e chama o pacote ou a biblioteca.

As bibliotecas carregadas na instância podem ser públicas ou particulares. Se a biblioteca for criada por um membro de `dbo`, a biblioteca será pública e poderá ser compartilhada com todos os usuários. Caso contrário, a biblioteca será particular somente para esse usuário.

## <a name="permissions"></a>Permissões

Requer a permissão `CREATE EXTERNAL LIBRARY`. Por padrão, todos os usuários que tenham o **dbo** ou que sejam membros da função **db_owner** têm permissões para criar uma biblioteca externa. Para todos os outros usuários, você deve conceder permissão explicitamente com uma instrução [GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql), especificando CREATE EXTERNAL LIBRARY como privilégio.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
No SQL Server 2019, além da permissão 'CREATE EXTERNAL LIBRARY', o usuário também precisa referenciar a permissão em uma linguagem externa para criar bibliotecas externas para essa linguagem externa.

```sql
GRANT REFERENCES ON EXTERNAL LANGUAGE::Java to user
GRANT CREATE EXTERNAL LIBRARY to user
```

::: moniker-end

Para modificar uma biblioteca, é necessário ter a permissão separada `ALTER ANY EXTERNAL LIBRARY`.

Para criar uma biblioteca externa usando um caminho de arquivo, o usuário precisa ter um logon autenticado pelo Windows ou ser membro da função de servidor fixa sysadmin.

## <a name="examples"></a>Exemplos

### <a name="a-add-an-external-library-to-a-database"></a>A. Adicionar uma biblioteca externa a um banco de dados  

O exemplo a seguir adiciona uma biblioteca externa chamada `customPackage` a um banco de dados.

```sql
CREATE EXTERNAL LIBRARY customPackage
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip') WITH (LANGUAGE = 'R');
```

Depois que a biblioteca é carregada com êxito na instância, um usuário executa o procedimento `sp_execute_external_script` para instalar a biblioteca.

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para a linguagem Python no SQL Server 2019, o exemplo também funciona, substituindo `'R'` com `'Python'`.
::: moniker-end

### <a name="b-installing-packages-with-dependencies"></a>B. Instalando pacotes com dependências

Se o pacote que você deseja instalar tiver dependências, será essencial que você analise as dependências de primeiro e segundo níveis e garanta que todos os pacotes estejam disponíveis _antes_ de tentar instalar o pacote de destino.

Por exemplo, suponha que você deseje instalar um novo pacote, `packageA`:

+ `packageA` tem uma dependência de `packageB`
+ `packageB` tem uma dependência de `packageC`

Para instalar o `packageA` com êxito, você precisa criar bibliotecas para o `packageB` e `packageC`, ao mesmo tempo adicionar `packageA` ao SQL Server. Lembre-se de verificar as versões de pacote também.

Na prática, as dependências do pacote para pacotes populares são geralmente muito mais complicadas do que esse exemplo simples. Por exemplo, **ggplot2** pode exigir mais de 30 pacotes e esses pacotes podem exigir pacotes adicionais que não estão disponíveis no servidor. Um pacote ausente ou uma versão de pacote incorreta pode causar falha na instalação.

Como pode ser difícil determinar todas as dependências apenas examinando o manifesto do pacote, recomendamos usar um pacote, como o [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html), para identificar todos os pacotes que podem ser necessários para concluir a instalação com êxito.

+ Carregue o pacote de destino e suas dependências. Todos os arquivos devem estar em uma pasta que seja acessível ao servidor.

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    GO

    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    GO

    CREATE EXTERNAL LIBRARY packageC FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageC.zip') 
    WITH (LANGUAGE = 'R');
    GO
    ```

+ Instale os pacotes necessários primeiro.

    Se um pacote obrigatório já foi carregado na instância, você não precisa adicioná-lo novamente. Verifique se o pacote existente é a versão correta. 
    
    Os pacotes `packageC` e `packageB` necessários são instalados na ordem correta, quando `sp_execute_external_script` é executado pela primeira vez para instalar o pacote `packageA`.

    No entanto, se um pacote obrigatório não estiver disponível, a instalação do pacote de destino `packageA` falhará.

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load the desired package packageA
    library(packageA)
    '
    ```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para a linguagem Python no SQL Server 2019, o exemplo também funciona, substituindo `'R'` com `'Python'`.
::: moniker-end

### <a name="c-create-a-library-from-a-byte-stream"></a>C. Criar uma biblioteca com base em um fluxo de bytes

Se você não tem a capacidade de salvar os arquivos de pacote em um local no servidor, pode passar o conteúdo do pacote em uma variável. O exemplo a seguir cria uma biblioteca, passando os bits como um literal hexadecimal.

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para a linguagem Python no SQL Server 2019, o exemplo também funciona, substituindo **'R'** com **'Python'** .
::: moniker-end

> [!NOTE]
> Este exemplo de código demonstra apenas a sintaxe; o valor binário em `CONTENT =` foi truncado para facilitar a leitura e não cria uma biblioteca de trabalho. O conteúdo real da variável binária deveria ser maior.

### <a name="d-change-an-existing-package-library"></a>D. Alterar uma biblioteca de pacote existente

A instrução DDL `ALTER EXTERNAL LIBRARY` pode ser usada para adicionar um novo conteúdo da biblioteca ou modificar o conteúdo da biblioteca existente. Para modificar uma biblioteca existente, é necessário ter a permissão `ALTER ANY EXTERNAL LIBRARY`.

Para obter mais informações, consulte [ALTER EXTERNAL LIBRARY](alter-external-library-transact-sql.md).

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="e-add-a-java-jar-file-to-a-database"></a>E. Adicionar um arquivo .jar do Java a um banco de dados  

O exemplo a seguir adiciona um arquivo jar externo chamado `customJar` a um banco de dados.

```sql
CREATE EXTERNAL LIBRARY customJar
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\customJar.jar') 
WITH (LANGUAGE = 'Java');
```

Depois que a biblioteca é carregada com êxito na instância, um usuário executa o procedimento `sp_execute_external_script` para instalar a biblioteca.

```sql
EXEC sp_execute_external_script
    @language = N'Java'
    , @script = N'customJar.MyCLass.myMethod'
    , @input_data_1 = N'SELECT * FROM dbo.MyTable'
WITH RESULT SETS ((column1 int))
```

### <a name="f-add-an-external-package-for-both-windows-and-linux"></a>F. Adicionar um pacote externo para o Windows e o Linux

Você pode especificar até dois `<file_spec>`, um para o Windows e outro para o Linux.

```sql
CREATE EXTERNAL LIBRARY lazyeval 
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\packageA.zip', PLATFORM = WINDOWS),
(CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\packageA.tar.gz', PLATFORM = LINUX)
WITH (LANGUAGE = 'R')
```

Quando você usar `sp_execute_external_script` para instalar o pacote, dependendo da plataforma na qual a Instância do SQL Server está em execução, o conteúdo da biblioteca dessa plataforma será usado.

```sql
EXECUTE sp_execute_external_script 
    @LANGUAGE = N'R',
    @SCRIPT = N'
library(packageA)
```
::: moniker-end

## <a name="see-also"></a>Confira também

[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
