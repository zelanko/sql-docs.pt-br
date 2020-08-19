---
description: MSSQLSERVER_2527
title: MSSQLSERVER_2527 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2687cc34a789723aeb9c098d622fbcd648ad0622
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428748"
---
# <a name="mssqlserver_2527"></a>MSSQLSERVER_2527
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|2527|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|Texto da mensagem|Não foi possível processar o índice I_NAME da tabela O_NAME porque o grupo de arquivos F_NAME está offline.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem informativa indica que não foi possível verificar o índice porque um dos grupos de arquivos que armazena dados para o índice está offline. O estado dos arquivos em um grupo de arquivos determina a disponibilidade de todo o grupo. Para que um grupo de arquivos fique disponível, todos os seus arquivos devem estar online. Se não houver outros problemas, todos os demais índices do mesmo objeto serão verificados.  
  
## <a name="user-action"></a>Ação do usuário  
Para exibir o estado dos arquivos do grupo de arquivos especificado, consulte a exibição do catálogo **sys.database_files** ou **sys.master_files**.  
  
Restaure o arquivo offline de um backup.  
  
## <a name="see-also"></a>Consulte Também  
[sys.database_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[sys.master_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
