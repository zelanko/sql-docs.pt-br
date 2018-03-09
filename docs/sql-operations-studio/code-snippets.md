---
title: "Criar trechos de código no Studio de operações do SQL (visualização) | Microsoft Docs"
description: "Saiba como criar e usar trechos de código SQL no Studio de operações do SQL (visualização)"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.reviewer: alayu; erickang; sstein
ms.prod: sql-non-specified
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4670c824b1e52776c3d81d097beeb4ccd9e62e2d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>Criar e usar trechos de código para criar rapidamente scripts Transact-SQL (T-SQL)[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Trechos de código de código [!INCLUDE[name-sos](../includes/name-sos-short.md)] são modelos que tornam mais fácil criar bancos de dados e objetos de banco de dados. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]fornece vários trechos de código do T-SQL para ajudar a gerar rapidamente a sintaxe apropriada. 

Trechos de código definido pelo usuário também podem ser criados.

## <a name="using-built-in-t-sql-code-snippets"></a>Usando trechos de código internos do T-SQL

1. Para acessar os trechos de código disponíveis, digite *sql* no editor de consultas para abrir a lista:

   ![trechos](media/code-snippets/sql-snippets.png)

1. Selecione o trecho de código que você deseja usar e gera o script T-SQL. Por exemplo, selecione *sqlCreateTable*:

   ![Criar tabela de trechos de código](media/code-snippets/create-table.png)

1. Atualize os campos realçados com seus valores específicos. Por exemplo, substitua *TableName* e *esquema* com os valores do banco de dados:

   ![Substitua o campo de modelo](media/code-snippets/table-from-snippet.png)

   Se o campo que você deseja alterar não é realçado (Isso ocorre ao mover o cursor em torno do editor), clique com botão direito a palavra que você deseja alterar e selecione **alterar todas as ocorrências**:

   ![Substitua o campo de modelo](media/code-snippets/change-all.png)

1. Atualizar ou adicionar qualquer T-SQL adicional necessários para o trecho de código selecionado. Por exemplo, atualizar *Column1*, *Column2*e adicionar mais colunas.


 
## <a name="creating-sql-code-snippets"></a>Criar trechos de código SQL 

Você pode definir seus próprios trechos. Para abrir o arquivo de trecho de código do SQL para edição:

1. Abra o *paleta do comando* (**Shift + Ctrl + P**) e o tipo *recorte*e selecione **preferências: Abra trechos de código do usuário**:

   ![Substitua o campo de modelo](media/code-snippets/user-snippets.png)

1. Selecione **SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)]herda sua funcionalidade de trecho de código do código do Visual Studio para que este artigo aborda especificamente usando trechos de código do SQL. Para obter mais informações, consulte [criar seus próprios trechos](https://code.visualstudio.com/docs/editor/userdefinedsnippets) na documentação do código do Visual Studio. 

   ![Substitua o campo de modelo](media/code-snippets/select-sql.png)

1. Cole o seguinte código em *sql.json*:

   ```sql
   "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "   $1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "   Column1 [NVARCHAR](50) NOT NULL,",
    "   Column2 [NVARCHAR](50) NOT NULL",
    "   -- specify more columns here",
    ");",
    "GO"
    ],
   "description": "User-defined snippet example 2"
   }
   ```

1. Salve o arquivo sql.json.
1. Abrir uma nova janela do editor de consultas clicando **Ctrl + N**.
2. Tipo **sql**, e você vê os trechos de código do usuário de dois recém-adicionado; *sqlCreateTable2* e *sqlSelectTop5*.

Selecione um dos novos trechos e dê a ele uma execução de teste!


## <a name="additional-resources"></a>Recursos adicionais

Para obter informações sobre o editor SQL, consulte [tutorial do editor de código](tutorial-sql-editor.md).