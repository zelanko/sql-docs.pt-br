---
title: Caixa de diálogo Adicionar Tabela (designers de consultas e de exibição)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.query.addtable
- vdtsql.chm:65565
ms.assetid: fce7adcc-4cf5-4a52-9203-11c13d1ecf08
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 47ded1289c8daec463913060ce205c162143eeb1
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002510"
---
# <a name="add-table-dialog-box-query-and-view-designers-visual-database-tools"></a>Caixa de diálogo Adicionar Tabela (Designers de Consulta e Exibição) (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
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
  
