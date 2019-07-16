---
title: Criar trechos de código reutilizáveis
titleSuffix: Azure Data Studio
description: Saiba como criar e usar trechos de código SQL no estúdio de dados do Azure
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 09a8432d10a70bb8530654d76bce874f735788a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959708"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>Criar e usar trechos de código para criar rapidamente scripts Transact-SQL (T-SQL) [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Trechos de código no [!INCLUDE[name-sos](../includes/name-sos-short.md)] são modelos que tornam fácil para criar bancos de dados e objetos de banco de dados. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] fornece vários trechos de código T-SQL para ajudar a gerar rapidamente a sintaxe apropriada. 

Trechos de código definido pelo usuário também podem ser criados.

## <a name="using-built-in-t-sql-code-snippets"></a>Usando trechos de código internos do T-SQL

1. Para acessar os trechos de código disponíveis, digite *sql* no editor de consultas para abrir a lista:

   ![trechos](media/code-snippets/sql-snippets.png)

1. Selecione o trecho de código que você deseja usar e gera o script T-SQL. Por exemplo, selecione *sqlCreateTable*:

   ![criar trechos de código de tabela](media/code-snippets/create-table.png)

1. Atualize os campos realçados com seus valores específicos. Por exemplo, substitua *TableName* e *esquema* com os valores do banco de dados:

   ![Substitua o campo de modelo](media/code-snippets/table-from-snippet.png)

   Se o campo que você deseja alterar não é realçado (isso acontece ao mover o cursor em torno do editor), com a palavra que você deseja alterar e selecione o botão direito **alterar todas as ocorrências**:

   ![Substitua o campo de modelo](media/code-snippets/change-all.png)

1. Atualizar ou adicionar qualquer T-SQL adicional necessários para o trecho de código selecionado. Por exemplo, atualize *Column1*, *Column2*e adicionar mais colunas.


 
## <a name="creating-sql-code-snippets"></a>Criar trechos de código do SQL 

Você pode definir seus próprios trechos. Para abrir o arquivo de trecho de código SQL para edição:

1. Abra o *paleta de comandos* (**Ctrl + Shift + P**) e o tipo *recorte*e selecione **preferências: Abra os trechos de código do usuário**:

   ![Substitua o campo de modelo](media/code-snippets/user-snippets.png)

1. Selecione **SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)] herda sua funcionalidade de trecho de código do Visual Studio Code para que este artigo aborda especificamente usando trechos de código SQL. Para obter mais informações, consulte [criando seus próprios trechos](https://code.visualstudio.com/docs/editor/userdefinedsnippets) na documentação do Visual Studio Code. 

   ![Substitua o campo de modelo](media/code-snippets/select-sql.png)

1. Cole o seguinte código no *sql.json*:

   ```sql
   {
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
   }
   ```

1. Salve o arquivo sql.json.
1. Abra uma nova janela do editor de consultas clicando **Ctrl + N**.
2. Tipo de **sql**, e você verá os trechos de código de dois usuário que você acabou de adicionar; *sqlCreateTable2* e *sqlSelectTop5*.

Selecione um dos novos trechos de código e dê a ele uma execução de teste!


## <a name="additional-resources"></a>Recursos adicionais

Para obter informações sobre o editor SQL, consulte [tutorial do editor de código](tutorial-sql-editor.md).
