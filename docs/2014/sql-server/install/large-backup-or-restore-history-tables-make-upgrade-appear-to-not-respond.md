---
title: Tabelas grandes de histórico de backup ou restauração tornar a atualização pareça não responder | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- backup history tables
- history tables
ms.assetid: f88d86ec-324b-4518-b6d7-1af7e7265812
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b29dc4e8f6dc32a1bda1ace7f029e77d8b1a45b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301472"
---
# <a name="large-backup-or-restore-history-tables-make-upgrade-appear-to-not-respond"></a>Tabelas grandes de histórico de restauração ou backup fazem com que a atualização pareça não responder
  No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], foram acrescentadas novas colunas a algumas tabelas de histórico de restauração e backup. Para atualizar essas tabelas, é necessário alterá-las para adicionar as novas colunas. Se uma ou mais tabelas tiverem um grande número de linhas, a atualização ficará parada por um tempo significativo na instrução ALTER TABLE, que é a instrução que adiciona colunas à tabela.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Tabelas grandes de histórico de restauração ou backup fazem com que a atualização pareça estar parade:  
  
-   **backupfile**  
  
-   **backupmediafamily**  
  
-   **backupmediaset**  
  
-   **backupset**  
  
-   **restorefile**  
  
-   **restorefilegroup**  
  
-   **restorehistory**  
  
 Se quaisquer destas tabelas tiver 10.000 linhas ou mais, o Supervisor de Atualização reportará uma falha de não conformidade. Ele não informará qual tabela excede o número de linhas permitido. A primeira tabela que exceder 10.000 linhas causará a falha.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes de atualizar um banco de dados, recomendamos que reduza o número de linhas para 10.000 caso uma tabela tenha mais linhas do que o especificado. Para reduzir as linhas em todas essas tabelas, você pode executar o **sp_delete_backuphistory** procedimento armazenado. Esse procedimento exclui as entradas de todas as tabelas de histórico de restauração e backup para grupos de backup mais antigos do que a data especificada. Para obter mais informações, consulte [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql).  
  
> [!NOTE]  
>  Você pode atualizar um banco de dados cujas tabelas de histórico de restauração e backup tenham mais de 10.000 linhas. Mas a atualização pode parecer estar parada enquanto essas tabelas grandes estiverem sendo alteradas. Quanto maior a tabela, mais tempo a Instalação levará para ser concluída.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
