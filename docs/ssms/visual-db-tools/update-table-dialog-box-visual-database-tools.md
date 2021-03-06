---
description: Caixa de diálogo Atualizar Tabela (Visual Database Tools)
title: Caixa de diálogo Atualizar Tabela
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 93c0ed1368325ec27ff9ebb640f48ee45f7de8ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88369172"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>Caixa de diálogo Atualizar Tabela (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Essa caixa de diálogo lhe permite especificar a tabela a ser atualizada.

Essa caixa de diálogo aparece se mais de uma tabela forem exibidas no painel Diagrama quando o tipo de consulta é mudado para consulta Update.  

Selecione a tabela a ser atualizada, depois clique em **OK**.

> [!NOTE]
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.

## <a name="see-also"></a>Consulte Também

[Criar consultas de atualização](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)
