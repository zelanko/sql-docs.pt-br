---
title: Adicionar caixa de diálogo de tabela (Designers de consulta e exibição) (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdt.dlgbox.query.addtable
- vdtsql.chm:65565
ms.assetid: fce7adcc-4cf5-4a52-9203-11c13d1ecf08
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8679c4a7210297b9bbf2c7245e7ce05a01d57a40
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119255"
---
# <a name="add-table-dialog-box-query-and-view-designers-visual-database-tools"></a>Caixa de diálogo Adicionar Tabela (Designers de Consulta e Exibição) (Visual Database Tools)
  Essa caixa de diálogo permite que você adicione tabelas, exibições, funções definidas pelo usuário ou sinônimos a uma consulta ou exibição.  
  
> [!NOTE]  
>  Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
