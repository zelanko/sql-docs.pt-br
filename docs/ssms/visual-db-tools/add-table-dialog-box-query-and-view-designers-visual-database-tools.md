---
title: Caixa de diálogo Adicionar Tabela (Designers de Consulta e Exibição) (Ferramentas de BD Visual) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.query.addtable
- vdtsql.chm:65565
ms.assetid: fce7adcc-4cf5-4a52-9203-11c13d1ecf08
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6d8b46182d226c2753d6b6d7366e47a305fdae28
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738784"
---
# <a name="add-table-dialog-box-query-and-view-designers-visual-database-tools"></a>Caixa de diálogo Adicionar Tabela (Designers de Consulta e Exibição) (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Essa caixa de diálogo permite que você adicione tabelas, exibições, funções definidas pelo usuário ou sinônimos a uma consulta ou exibição.  
  
> [!NOTE]  
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="options"></a>Opções  
**Tabelas**  
Lista as tabelas que você pode adicionar ao painel **Diagrama** . Para adicionar uma tabela, selecione-a e clique em **Adicionar**. Para adicionar várias tabelas de uma vez, selecione-as e clique em **Adicionar**.  
  
**Exibições**  
Lista os modos de exibição que você pode adicionar ao painel **Diagrama** . Para adicionar um modo de exibição, selecione-o e clique em **Adicionar**. Para adicionar vários modos de exibição de uma vez, selecione-os e clique em **Adicionar**.  
  
**Funções**  
Lista as funções definidas pelo usuário que você pode adicionar ao painel **Diagrama** . Para adicionar uma função, selecione-a e clique em **Adicionar**. Para adicionar várias funções de uma vez, selecione-as em clique em **Adicionar**.  
  
**Sinônimos**  
Lista os sinônimos que você pode adicionar ao painel **Diagrama** . Para adicionar um sinônimo, selecione-o e clique em **Adicionar**. Para adicionar vários sinônimos de uma vez, selecione-os em clique em **Adicionar**.  
  
**Atualizar**  
Atualiza a lista para incluir qualquer alteração feita ao banco de dados desde que a lista foi recuperada pela última vez.  
  
**Adicionar**  
Adiciona o item ou itens selecionados.  
  
## <a name="see-also"></a>Consulte Também  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
