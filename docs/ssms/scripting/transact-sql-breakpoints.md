---
title: Pontos de interrupção Transact-SQL
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1c31101eb201a55dffd100fb9365f7c29826fb5d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75243399"
---
# <a name="transact-sql-breakpoints"></a>Pontos de interrupção Transact-SQL

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Os pontos de interrupção especificam que o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] pause a execução em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] específica, para que você possa ver o estado dos elementos do código nesse ponto.

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="breakpoints"></a>Pontos de interrupção

Ao executar o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] , você pode alternar um ponto de interrupção em instruções específicas. Quando a execução alcançar uma instrução com um ponto de interrupção, o depurador pausará a execução para que você possa exibir informações de depuração, como os valores presentes em variáveis e parâmetros.

Você pode gerenciar pontos de interrupção individualmente na janela de editor, ou em conjunto, usando a janela **Pontos de interrupção** . Você pode editar pontos de interrupção para especificar itens, como as condições específicas sob as quais a execução deve pausar, ou as ações a serem adotadas se o ponto de interrupção for executado.

## <a name="breakpoint-tasks"></a>Tarefas de ponto de interrupção  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como especificar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] na qual você deseja que o depurador pause.|[Alternar um ponto de interrupção](../../relational-databases/scripting/toggle-a-breakpoint.md)|  
|Descreve como desativar um ponto de interrupção temporariamente e, posteriormente, reativá-lo. Também descreve como excluir um ponto de interrupção.|[Habilitar, desabilitar e excluir pontos de interrupção](../../relational-databases/scripting/enable-disable-and-delete-breakpoints.md)|  
|Descreve como especificar uma condição, que define se o ponto de interrupção é interrompido com base na avaliação de uma expressão Transact-SQL especificada.|[Especificar uma condição de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-condition.md)|  
|Descreve como especificar uma contagem de ocorrências, que leva um ponto de interrupção a ser interrompido somente quando a instrução que contém o ponto de interrupção é executada um número especificado de vezes.|[Especificar uma contagem de ocorrências](../../relational-databases/scripting/specify-a-hit-count.md)|  
|Descreve como especificar um filtro, o que leva um ponto de interrupção a ser interrompido somente para processos ou threads especificados.|[Especificar um filtro de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-filter.md)|  
|Descreve como especificar uma ação **When Hit** , que é uma operação personalizada executada quando a instrução de ponto de interrupção é executada. Um exemplo seria a impressão de uma mensagem.|[Especificar uma ação de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-action.md)|  
|Descreve como editar o local de um ponto de interrupção.|[Editar um local de ponto de interrupção](../../relational-databases/scripting/edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Informações do depurador Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)  
  
  
