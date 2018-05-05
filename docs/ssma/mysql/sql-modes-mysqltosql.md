---
title: Modos SQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fc24d212fe2f5e45ff349c404671ffea71a7c490
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-modes-mysqltosql"></a>Modos SQL (MySQLToSQL)
O SSMA para MySQL pode operar em diferentes modos SQL e pode aplicar esses modos de forma diferente para diferentes clientes.  
  
Modos de definem a sintaxe SQL que deve ter suporte MySQL e verifica se o tipo de validação de dados deve executar. Isso torna mais fácil de usar MySQL em diferentes ambientes e use o MySQL com o SQL Server.  
  
## <a name="sql-modes-grid"></a>Grade de modos SQL:  
  
-   Grade de modos SQL no nível raiz contém as seguintes colunas: **nome do modo SQL**, **carregado SQL modos**, e **efetivo modos de SQL**.  
  
-   Grade de modos SQL em bancos de dados categoria, banco de dados, tabela categoria, categoria de instruções, categoria de modos de exibição, tabela, exibição, funções, procedimentos, UDF e nível de objeto de evento contém as seguintes colunas: **nome do modo SQL**, **modos de SQL herdadas**, e **efetivo modos de SQL**.  
  
-   Grade de modos SQL no nível de procedimento armazenado, função armazenado e disparador contém as seguintes colunas: **nome do modo SQL**, **modos Original do SQL**, e **efetivo modos de SQL**.  
  
> [!NOTE]  
> Modos de grupo serão mostrados em negrito, abaixo da coluna 'Nome do modo SQL'.  
  
## <a name="loaded-sql-modes"></a>Modos SQL carregado  
Esses são os modos SQL, que são definidos no nível de sessão ou raiz. Os modos SQL carregado uma vez para o banco de dados de destino não pode ser editados ou modificados.  
  
## <a name="inherited-sql-modes"></a>Modos SQL herdadas  
Esses são os modos SQL, que são herdadas a partir do nó pai correspondente.  
  
Exceto para a categoria de funções, categoria de procedimentos, categoria de eventos e gatilhos, esses modos SQL estão presentes em todos os níveis (objeto de banco de dados, tabela categoria, categoria de instruções, modos de exibição categoria, tabela, exibição, funções, procedimentos, UDF e eventos).  
  
> [!NOTE]  
> Selecionando o **herdar do pai** caixa de seleção, modos de SQL herdadas pode ser herdada do nó pai. Por padrão, essa caixa de seleção permanece selecionada.  
  
## <a name="original-sql-modes"></a>Modos SQL originais  
Esses são os modos SQL presentes em apenas os níveis de função, o procedimento e o gatilho.  
  
> [!NOTE]  
> Selecionando o **Use original** verificar caixa, os modos de SQL que foram usadas originalmente para a função correspondente ou procedimento ou gatilho pode ser usado. Por padrão, essa caixa de seleção permanece selecionada.  
  
## <a name="effective-sql-modes"></a>Modos SQL efetiva  
Modos de SQL efetivo pode ser definidos em vários níveis da seguinte maneira:  
  
-   **No nível de sessão:**  
  
    1.  Todos os modos SQL carregado pode ser chamados, "Modos de SQL efetivo".  
  
    2.  Nesse nível, os modos SQL efetivos podem ser diretamente e explicitamente modificados.  
  
    3.  O modo efetivo do SQL que é definido explicitamente não é refletido como carregar o modo SQL e, por fim, é aplicado ao objeto.  
  
-   **No nível de função ou procedimento ou Gatilho:**  
  
    1.  Todos os modos SQL Original pode ser chamado, "Modos de SQL efetivo".  
  
    2.  Nesse nível, de modo efetivo do SQL pode ser explicitamente modificado apenas quando o **Use original** caixa de seleção está desmarcada.  
  
    3.  O modo efetivo do SQL que é definido explicitamente não é refletido como modo Original do SQL e, por fim, é aplicado ao objeto.  
  
-   **Em nós que não seja o nível de função ou procedimento ou Gatilho:**  
  
    1.  Todos os modos SQL herdadas pode ser chamados, "Modos de SQL efetivo".  
  
    2.  Nesse nível, de modo efetivo do SQL pode ser explicitamente modificado apenas quando o **herdar do pai** caixa de seleção está desmarcada.  
  
    3.  O modo efetivo do SQL que é definido explicitamente não é refletido como modo herdado do SQL e, por fim, é aplicado ao objeto.  
  
