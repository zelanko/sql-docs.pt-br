---
description: MSSQLSERVER_3859
title: MSSQLSERVER_3859
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3859 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 4a3857e9e98bfbe7fcc86ee07272698f0fcac763
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418647"
---
# <a name="mssqlserver_3859"></a>MSSQLSERVER_3859
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|3859|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|DBCC_CHECKCAT_DIRECT_UPDATE|
|Texto da mensagem|Aviso: o catálogo do sistema foi atualizado diretamente na ID de banco de dados \%d, mais recentemente em %S_DATE|
||

## <a name="explanation"></a>Explicação

Esse erro indica uma alteração iniciada pelo usuário nas tabelas do sistema. Não há suporte para a atualização manual de tabelas do sistema. As tabelas do sistema só devem ser atualizadas pelo mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detecta alterações iniciadas pelo usuário nas tabelas do sistema, o erro 3859 é gerado nos dois seguintes cenários:

- Cenário 1

    Um evento semelhante ao seguinte é registrado no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no log do aplicativo do Visualizador de Eventos quando você inicia um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém uma tabela do sistema que foi atualizada manualmente:

    > Nome do Log: Aplicativo  
    Origem: ID de Evento do MSSQLSERVER: 3859  
    Categoria da tarefa: Servidor  
    Nível: Informações  
    Descrição: Aviso: o catálogo do sistema foi atualizado diretamente na ID de banco de dados \%d, mais recentemente em **date_time**  

- Cenário 2  

    A seguinte mensagem de aviso é retornada quando você executa o comando `DBCC_CHECKDB` depois que uma tabela do sistema é atualizada manualmente:

    > Resultados do DBCC para ' **database_name** '.  
    Mensagem 8992, Nível 16, Estado 1, Linha 1  
    Verifique a Mensagem do Catálogo 3859, Estado 1: Aviso: o catálogo do sistema foi atualizado diretamente na ID de banco de dados \%d, mais recentemente em **date_time** .  
    CHECKDB encontrou 0 erros de alocação e 0 erros de consistência no banco de dados ' **db_name** '.  
    A execução do DBCC foi concluída. Se o DBCC imprimiu mensagens de erro, contate o administrador do sistema.

## <a name="user-action"></a>Ação do usuário

Para resolver esse problema, use um dos métodos a seguir.

- Método 1

    Caso você tenha um backup limpo do banco de dados, restaure o banco de dados do backup.  
    > [!NOTE]
    > Esse método só funcionará se o backup não tiver inconsistências nos metadados.  

- Método 2  

    Caso você não possa restaurar o banco de dados por meio de um backup, exporte os dados e os objetos para um novo banco de dados. Em seguida, transfira o conteúdo do banco de dados atualizado manualmente para o novo banco de dados. Observe que não é possível reparar as inconsistências nos catálogos do sistema usando as opções REPAIR nos comandos DBCC CHECKDB. Portanto, como o comando não pode reparar os metadados corrompidos, o comando não fornece nenhum nível de reparo recomendado.

    > [!NOTE]
    > Veja os dados nas tabelas do sistema por meio das exibições do catálogo do sistema.

## <a name="more-information"></a>Mais informações

Para obter mais informações, confira: [Tabelas base do sistema](/sql/relational-databases/system-tables/system-base-tables).
