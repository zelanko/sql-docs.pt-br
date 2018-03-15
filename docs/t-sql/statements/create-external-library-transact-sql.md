---
title: CREATE EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/25/2018
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
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: e28716314837225586cf4bd1f80a37c5c6b824ab
ms.sourcegitcommit: 6e819406554efbd17bbf84cf210d8ebeddcf772d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="create-external-library-transact-sql"></a>CREATE EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

Carrega os pacotes do R em um banco de dados do caminho de arquivo ou fluxo de bytes especificado.

Essa instrução funciona como um mecanismo genérico para que o administrador de banco de dados faça o upload dos artefatos necessários para novos tempos de execução de idiomas externos (R, Python, Java, etc.) e plataformas de sistema operacional compatíveis com o [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. 

Atualmente, há compatibilidade apenas com a linguagem R e a plataforma Windows. O suporte para o Python e Linux está previsto para uma versão posterior.

## <a name="syntax"></a>Sintaxe

```text
CREATE EXTERNAL LIBRARY library_name  
    [ AUTHORIZATION owner_name ]  
FROM <file_spec> [,…2]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
(CONTENT = { <client_library_specifier> | <library_bits> }  
[, PLATFORM = WINDOWS ])  
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

As bibliotecas são adicionadas ao banco de dados no escopo do usuário. Ou seja, os nomes de biblioteca são considerados exclusivos no contexto de um usuário ou de um proprietário específico e devem ser exclusivos por usuário. Por exemplo, dois usuários **RUser1** e **RUser2** podem individual e separadamente carregar a biblioteca do R `ggplot2`.

Os nomes de biblioteca não podem ser atribuídos arbitrariamente; o nome da biblioteca deve ter o mesmo nome necessário para carregar a biblioteca do R por meio do R.

**owner_name**

Especifica o nome do usuário ou da função que é a proprietária da biblioteca externa. Se não estiver especificada, a propriedade será dada ao usuário atual.

As bibliotecas que pertencem ao proprietário do banco de dados são consideradas globais para o banco de dados e o tempo de execução. Em outras palavras, os proprietários do banco de dados podem criar bibliotecas que contêm um conjunto comum de bibliotecas ou pacotes que são compartilhados por muitos usuários. Quando uma biblioteca externa é criada por um usuário diferente do usuário `dbo`, a biblioteca externa é particular somente a esse usuário.

Quando o usuário **RUser1** executa um script R, o valor de `libPath` pode conter vários caminhos. O primeiro caminho é sempre o caminho para a biblioteca compartilhada criado pelo proprietário do banco de dados. A segunda parte de `libPath` especifica o caminho que contém os pacotes carregados individualmente por **RUser1**.

**file_spec**

Especifica o conteúdo do pacote para uma plataforma específica. Há compatibilidade apenas com um artefato de arquivo por plataforma.

O arquivo pode ser especificado no formato de um caminho local ou caminho de rede.

Opcionalmente, uma plataforma de sistema operacional para o arquivo pode ser especificada. Somente um artefato ou conteúdo de arquivo é permitido para cada plataforma de sistema operacional em uma linguagem ou um tempo de execução específico.

**library_bits**

Especifica o conteúdo do pacote como um literal hexadecimal, semelhante aos assemblies. 

Essa opção será útil se você precisar criar uma biblioteca ou alterar uma biblioteca existente (e tiver as permissões necessárias para fazer isso), mas o sistema de arquivos no servidor for restrito e você não puder copiar os arquivos de biblioteca para um local que o servidor possa acessar.

**PLATFORM = WINDOWS**

Especifica a plataforma para o conteúdo da biblioteca. O valor usa como padrão a plataforma de host na qual o SQL Server está sendo executado. Portanto, o usuário não precisa especificar o valor. É necessário no caso em que várias plataformas são compatíveis ou quando o usuário precisa especificar outra plataforma. 

no SQL Server 2017, o Windows é a única plataforma compatível.

## <a name="remarks"></a>Remarks

Para a linguagem R, ao usar um arquivo, os pacotes precisam ser preparados no formato de arquivos mortos compactados com a extensão .ZIP para o Windows. Atualmente, há compatibilidade apenas com a plataforma Windows. 

A instrução `CREATE EXTERNAL LIBRARY` carrega os bits de biblioteca no banco de dados. A biblioteca é instalada quando um usuário executa um script externo usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e chama o pacote ou a biblioteca.

As bibliotecas carregadas na instância podem ser públicas ou particulares. Se a biblioteca for criada por um membro de `dbo`, a biblioteca será pública e poderá ser compartilhada com todos os usuários. Caso contrário, a biblioteca será particular somente para esse usuário.

Não é possível usar blobs como uma fonte de dados na versão SQL Server 2017.

## <a name="permissions"></a>Permissões

Requer a permissão `CREATE ANY EXTERNAL LIBRARY`.

Para modificar uma biblioteca, é necessário ter a permissão separada, `ALTER ANY EXTERNAL LIBRARY`.

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

### <a name="b-installing-packages-with-dependencies"></a>B. Instalando pacotes com dependências

Se o pacote que você deseja instalar tiver dependências, será essencial que você analise as dependências de primeiro e segundo níveis e garanta que todos os pacotes estejam disponíveis _antes_ de tentar instalar o pacote de destino.

Por exemplo, suponha que você deseje instalar um novo pacote, `packageA`:

+ `packageA` tem uma dependência de `packageB`
+ `packageB` tem uma dependência de `packageC`

Para instalar o `packageA` com êxito, você precisa criar bibliotecas para o `packageB` e `packageC`, ao mesmo tempo adicionar `packageA` ao SQL Server. Lembre-se de verificar as versões de pacote também.

Na prática, as dependências do pacote para pacotes populares são geralmente muito mais complicadas do que esse exemplo simples. Por exemplo, ggplot2 pode exigir mais de 30 pacotes, e esses pacotes podem exigir pacotes adicionais que não estão disponíveis no servidor. Um pacote ausente ou uma versão de pacote incorreta pode causar falha na instalação.

Como pode ser difícil determinar todas as dependências apenas examinando o manifesto do pacote, recomendamos o uso de um pacote como [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) ou [iGraph](http://igraph.org/redirect.html) para identificar todos os pacotes que podem ser necessários para concluir a instalação com êxito.

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
    # call function from package
    OutputDataSet <- packageA.function()
    '
    with result sets (([result] int));    
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>C. Criar uma biblioteca com base em um fluxo de bytes

Se você não tem a capacidade de salvar os arquivos de pacote em um local no servidor, também pode passar o conteúdo do pacote em uma variável. O exemplo a seguir cria uma biblioteca, passando os bits como um literal hexadecimal.

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

Aqui, os valores hexadecimais foram truncados para facilitar a leitura.

### <a name="d-change-an-existing-package-library"></a>D. Alterar uma biblioteca de pacote existente

A instrução DDL `ALTER EXTERNAL LIBRARY` pode ser usada para adicionar um novo conteúdo da biblioteca ou modificar o conteúdo da biblioteca existente. Para modificar uma biblioteca existente, é necessário ter a permissão `ALTER ANY EXTERNAL LIBRARY`.

Para obter mais informações, consulte [ALTER EXTERNAL LIBRARY](alter-external-library-transact-sql.md).

### <a name="e-delete-a-package-library"></a>E. Excluir uma biblioteca de pacote

Para excluir uma biblioteca de pacote do banco de dados, execute a instrução:

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

> [!NOTE]
> Ao contrário de outras instruções `DROP` no [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)], essa instrução é compatível com um parâmetro opcional que especifica a autoridade do usuário. Essa opção permite que os usuários com funções de propriedade excluam as bibliotecas carregadas por usuários normais.

## <a name="see-also"></a>Consulte também

[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
