---
description: MSSQLSERVER_17659
title: MSSQLSERVER_17659
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17659 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 5e4656c437e1b1a19382222107add8392e0c47e4
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418651"
---
# <a name="mssqlserver_17659"></a>MSSQLSERVER_17659
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|17659|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|DEMO_SYSCATUPDATE|
|Texto da mensagem|A ID de tabela do sistema \%d foi atualizada diretamente na ID de banco de dados \%d e a coerência do cache pode não ter sido mantida. <br/> O SQL Server deve ser reiniciado.|
||

## <a name="explanation"></a>Explicação

Esse erro indica que um objeto do sistema foi atualizado diretamente. Não há suporte para a atualização manual de tabelas do sistema. As tabelas do sistema só devem ser atualizadas pelo mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detecta alterações iniciadas pelo usuário nas tabelas do sistema, o erro 17659 é gerado. Um evento semelhante ao mostrado a seguir é registrado no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no log do aplicativo do Visualizador de Eventos neste cenário.

> Nome do Log: Aplicativo  
Origem: MSSQLServer  
ID de evento: 17659  
Categoria da tarefa: Servidor  
Nível: Informações  
Descrição: Aviso: a ID de tabela do sistema \%d foi atualizada diretamente na ID de banco de dados %d e a coerência do cache pode não ter sido mantida. O SQL Server deve ser reiniciado.

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
