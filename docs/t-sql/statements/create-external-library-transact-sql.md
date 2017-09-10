---
title: Criar biblioteca externa (Transact-SQL) | Microsoft Docs
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f11a6b7633be392e1f789e12c43f2e5d6e56b47
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-library-transact-sql"></a>Criar biblioteca externa (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

Carrega os pacotes de R para um banco de dados do caminho do arquivo ou fluxo de bytes especificado.

Essa instrução funciona como um mecanismo genérico para o administrador de banco de dados carregar os artefatos necessários para qualquer novo runtimes de idiomas externos (R, Python, Java, etc.) e plataformas de sistema operacional com suporte pelo [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. Atualmente, há suporte apenas a linguagem R e a plataforma Windows.

## <a name="syntax"></a>Sintaxe

```
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

**nome_da_biblioteca**

Bibliotecas forem adicionadas ao banco de dados com escopo para o usuário. Ou seja, nomes de biblioteca são considerados exclusivos dentro do contexto de um usuário específico ou um proprietário e nomes de biblioteca devem ser exclusivos por usuário. Por exemplo, dois usuários **RUser1** e **RUser2** podem ambos individualmente e separadamente carregar a biblioteca R `ggplot2`. 

**owner_name**

Especifica o nome do usuário ou função que possui a biblioteca externa. Se não estiver especificada, a propriedade será dada ao usuário atual.

As bibliotecas que pertencem ao proprietário do banco de dados são consideradas globais para o banco de dados e o tempo de execução. Em outras palavras, os proprietários do banco de dados podem criar bibliotecas que contenham um conjunto comum de bibliotecas ou pacotes que são compartilhados por muitos usuários. Quando uma biblioteca externa é criada por um usuário diferente do `dbo` usuário, a biblioteca externa é privada somente para esse usuário.   

Quando o usuário **RUser1** executa um script R, o valor de `libPath` pode conter vários caminhos. O primeiro caminho sempre é o caminho para a biblioteca compartilhada criada pelo proprietário do banco de dados. A segunda parte do `libPath` Especifica o caminho que contém os pacotes carregados individualmente por **RUser1**.

**file_spec**

Especifica o conteúdo do pacote para uma plataforma específica. Há suporte para o artefato de apenas um arquivo por plataforma. 

O arquivo pode ser especificado na forma de um caminho local ou caminho de rede.

Opcionalmente, uma plataforma de sistema operacional para o arquivo pode ser especificada. O artefato de apenas um arquivo ou o conteúdo é permitido para cada plataforma de sistema operacional para um idioma específico ou o tempo de execução.

**PLATAFORMA = WINDOWS**

Especifica a plataforma para o conteúdo da biblioteca. O valor padrão para a plataforma de host que está executando o SQL Server. Portanto, o usuário não precisa especificar o valor. É necessário no caso em que várias plataformas têm suporte ou o usuário precisa especificar uma plataforma diferente. Windows é a única plataforma com suporte.

## <a name="remarks"></a>Comentários

Para a linguagem R, os pacotes devem ser preparados na forma de arquivos compactados com o. Extensão ZIP para Windows. Atualmente, apenas a plataforma do Windows tem suporte.  

O `CREATE EXTERNAL LIBRARY` instrução carrega apenas os bits de biblioteca para o banco de dados. A biblioteca não está realmente instalada até que um usuário executa um script externo posteriormente, executando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  

## <a name="permissions"></a>Permissões  
Requer o `CREATE EXTERNAL LIBRARY` permissão.  

## <a name="examples"></a>Exemplos

### <a name="a-add-an-external-library-to-a-database"></a>A. Adicionar uma biblioteca externa para um banco de dados  
O exemplo a seguir adiciona uma biblioteca externa chamada customPackage para um banco de dados.   
```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
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

### <a name="b-installing-packages-with-dependencies"></a>B. Instalando pacotes com dependências

Se `packageB` tem uma dependência em `packageA`, em seguida, por exemplo, o código segue essas entidades gerais:   
```
CREATE EXTERNAL LIBRARY packageA 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R'); 

CREATE EXTERNAL LIBRARY packageB FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R');
```

`packageA`e `packageB` são instalados quando `sp_execute_external_script` é executado pela primeira vez.   
```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load packageB
library(packageB)

# call customPackageBFunc
OutputDataSet <- customPackageBFunc()
'
with result sets (([result] int));    
```

Para que isso funcione, a pasta onde os pacotes são salvos deve ser acessível para o servidor. 

### <a name="change-an-existing-package-library"></a>Alterar uma biblioteca de pacote existente

O `ALTER EXTERNAL LIBRARY` instrução DDL pode ser usada para adicionar o novo conteúdo da biblioteca ou modificar o conteúdo da biblioteca existente.   

### <a name="delete-a-package-library"></a>Excluir uma biblioteca de pacote

Para excluir uma biblioteca de pacote do banco de dados, execute a instrução:

```sql
DROP EXTERNAL LIBRARY ggplot2 <user_name>;
```

> [!NOTE]
> Ao contrário de outras `DROP` instruções [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)], esta instrução oferece suporte a um parâmetro opcional que especifica a autoridade do usuário. Essa opção permite que os usuários com as funções de propriedade excluir bibliotecas carregadas por usuários regulares. 

## <a name="see-also"></a>Consulte também  
[ALTER biblioteca externa (Transact-SQL)](alter-external-library-transact-sql.md)  
[SOLTE a biblioteca externa (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

