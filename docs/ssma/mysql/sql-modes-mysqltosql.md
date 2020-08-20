---
description: Modos SQL (MySQLToSQL)
title: Modos SQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8d0631b35d2631e04cfad5c509d6084ba0a30aaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497713"
---
# <a name="sql-modes-mysqltosql"></a>Modos SQL (MySQLToSQL)
O SSMA para MySQL pode operar em modos SQL diferentes e pode aplicar esses modos de forma diferente para clientes diferentes.  
  
Os modos definem a sintaxe SQL que o MySQL deve dar suporte e o tipo de verificações de validação de dados que ele deve executar. Isso torna mais fácil usar o MySQL em ambientes diferentes e usar o MySQL com SQL Server.  
  
## <a name="sql-modes-grid"></a>Grade de modos SQL:  
  
-   A grade de modos SQL no nível de raiz contém as seguintes colunas: **nome do modo SQL**, **modos SQL carregados**e **modos SQL efetivos**.  
  
-   As grades de modos SQL na categoria de bancos de dados Category, Database, tabela, Table Statements, as views categoria, Table, View, functions, Procedures, UDF e Event Object Level contêm as seguintes colunas: **SQL Mode Name**, **modos SQL herdados**e **modos SQL efetivos**.  
  
-   A grade de modos SQL no procedimento armazenado, na função armazenada e no nível de gatilho contém as seguintes colunas: **nome do modo SQL**,  **modos SQL originais**e **modos SQL efetivos**.  
  
> [!NOTE]  
> Os modos de grupo serão mostrados em negrito, sob a coluna ' nome do modo SQL '.  
  
## <a name="loaded-sql-modes"></a>Modos SQL carregados  
Esses são os modos SQL, que são definidos no nível de sessão ou raiz. Os modos SQL uma vez carregados no banco de dados de destino não podem ser editados ou modificados.  
  
## <a name="inherited-sql-modes"></a>Modos SQL herdados  
Esses são os modos SQL, que são herdados do nó pai correspondente.  
  
Exceto a categoria de funções, a categoria de procedimentos, a categoria de eventos e os gatilhos, esses modos SQL estão presentes em todos os níveis (banco de dados, categoria de tabela, categoria de instruções, categoria de exibições, tabela, exibição, funções, procedimentos, UDF e objeto de evento).  
  
> [!NOTE]  
> Ao marcar a caixa de seleção **herdar do pai** , os modos SQL herdados podem ser herdados do nó pai. Por padrão, essa caixa de seleção permanece selecionada.  
  
## <a name="original-sql-modes"></a>Modos SQL originais  
Esses são os modos SQL presentes somente em níveis de função, procedimento e gatilho.  
  
> [!NOTE]  
> Ao marcar a caixa de seleção **usar original** , os modos SQL que foram usados originalmente na função ou no gatilho correspondente podem ser usados. Por padrão, essa caixa de seleção permanece selecionada.  
  
## <a name="effective-sql-modes"></a>Modos SQL efetivos  
Os modos SQL efetivos podem ser definidos em vários níveis da seguinte maneira:  
  
-   **No nível da sessão:**  
  
    1.  Todos os modos SQL carregados podem ser chamados, "modos SQL efetivos".  
  
    2.  Nesse nível, os modos SQL efetivos podem ser diretamente e explicitamente modificados.  
  
    3.  O modo SQL efetivo definido explicitamente não é refletido como modo SQL carregado e, por fim, é aplicado ao objeto.  
  
-   **Em nível de função ou procedimento ou gatilho:**  
  
    1.  Todos os modos SQL originais podem ser chamados, "modos SQL efetivos".  
  
    2.  Nesse nível, o modo SQL efetivo pode ser explicitamente modificado somente quando a caixa de seleção **usar original** estiver desmarcada.  
  
    3.  O modo SQL efetivo definido explicitamente não é refletido como o modo SQL original e, por fim, é aplicado ao objeto.  
  
-   **Em nós diferentes de função ou procedimento ou nível de gatilho:**  
  
    1.  Todos os modos SQL herdados podem ser chamados, "modos SQL efetivos".  
  
    2.  Nesse nível, o modo SQL efetivo pode ser explicitamente modificado somente quando a caixa de seleção **herdar do pai** está desmarcada.  
  
    3.  O modo SQL efetivo definido explicitamente não é refletido como modo SQL herdado e, por fim, é aplicado ao objeto.  
  
