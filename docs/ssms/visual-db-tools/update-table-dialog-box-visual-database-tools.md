---
title: "Caixa de diálogo Atualizar Tabela (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e330c3d85c467248490f75fb23c3fabb8ca82c9c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="update-table-dialog-box-visual-database-tools"></a>Caixa de diálogo Atualizar Tabela (Visual Database Tools)
Essa caixa de diálogo lhe permite especificar a tabela a ser atualizada.  
  
Essa caixa de diálogo aparece se mais de uma tabela forem exibidas no painel Diagrama quando o tipo de consulta é mudado para consulta Update.  
  
Selecione a tabela a ser atualizada, depois clique em **OK**.\  
  
> [!NOTE]  
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="see-also"></a>Consulte também  
[Criar consultas de atualização (Visual Database Tools)](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)  
  
