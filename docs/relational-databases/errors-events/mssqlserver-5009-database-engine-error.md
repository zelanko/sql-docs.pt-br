---
description: MSSQLSERVER_5009
title: MSSQLSERVER_5009
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5009 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 1ca7fb52969d9ec08d8c80c48ec1325277a13fa7
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418663"
---
# <a name="mssqlserver_5009"></a>MSSQLSERVER_5009
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|5009|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|ALT_BADDISKS|
|Texto da mensagem|Um ou mais arquivos listados na instrução não foram encontrados ou não foram inicializados|
||

## <a name="explanation"></a>Explicação

Esse erro indica que você especificou uma fileID ou um nome de arquivo no comando ALTER DATABASE ou DBCC SHRINK* que não pôde ser resolvido.

Considere o seguinte cenário:

- Você tem um banco de dados do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa um modelo de recuperação bulk-logged ou completa.
- Você adiciona um novo arquivo de dados chamado *db_file1* ao banco de dados.
- Você define o tipo de arquivo do arquivo `db_file1` como dados.
- Você percebe que especificou o tipo de arquivo incorretamente.
- Você remove o arquivo `db_file1` e faz backup do log de transações desse banco de dados.
- Você adiciona um novo arquivo de log chamado *db_file1* ao mesmo banco de dados.
- Você tenta remover o arquivo de log chamado *db_file1* usando a instrução ALTER DATABASE ou usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio.

Neste cenário, você recebe uma mensagem de erro semelhante à seguinte:

> Mensagem 5009, Nível 16, Estado 9, Linha 1: um ou mais arquivos listados na instrução não foram encontrados ou não foram inicializados.

## <a name="possible-causes"></a>Possíveis causas

Esse problema ocorre se o nome lógico do arquivo que você tentar remover não for exclusivo nas tabelas do catálogo do sistema. Por exemplo, esse problema ocorre se o arquivo existia no banco de dados anteriormente e foi removido.

Quando você tenta remover um arquivo que tem o mesmo nome lógico, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta remover o arquivo lógico removido. Isso resulta na mensagem de erro.

## <a name="user-action"></a>Ação do usuário

Para encontrar uma solução alternativa para esse problema, siga estas etapas.

> [!NOTE]
> Essas etapas fazem com que os valores da ID de arquivo sejam reutilizados.

1. Use a instrução ALTER DATABASE para criar um arquivo lógico que tenha um nome diferente e o mesmo tipo de dados. Por exemplo, nomeie o arquivo lógico como `different_remove_file_name` em vez de `db_file1`, como no seguinte exemplo:

    ```sql
    ALTER DATABASE [DBNAME] ADD FILE ( NAME = N'different_remove_file_name',
    FILENAME = N'D:\MSSQL.1\MSSQL\DATA\db_file1.ndf', SIZE = 1MB, MAXSIZE = 1MB)
    ```

    > [!NOTE]
    > Você pode usar qualquer nome ou caminho de arquivo.

1. Use a instrução ALTER DATABASE para remover o arquivo lógico criado na etapa 1, como no seguinte exemplo:

    ```sql
    ALTER DATABASE [DBNAME] REMOVE FILE [different_remove_file_name]
    ```

1. Crie um backup de log de transações do banco de dados.
1. Tente remover o arquivo lógico chamado *db_file1* novamente.
