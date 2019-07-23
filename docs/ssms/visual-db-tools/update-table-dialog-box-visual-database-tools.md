---
title: Caixa de diálogo Atualizar Tabela (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f2c3c1b59b43458bf6f24e5c255f43d7eb4cd92e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263117"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>Caixa de diálogo Atualizar Tabela (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Essa caixa de diálogo lhe permite especificar a tabela a ser atualizada.  
  
Essa caixa de diálogo aparece se mais de uma tabela forem exibidas no painel Diagrama quando o tipo de consulta é mudado para consulta Update.  
  
Selecione a tabela a ser atualizada, depois clique em **OK**.\  
  
> [!NOTE]  
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="see-also"></a>Consulte Também  
[Criar consultas de atualização (Visual Database Tools)](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)  
  
