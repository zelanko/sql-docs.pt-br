---
title: Gerenciando Backups (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Managing Backups
ms.assetid: 266d987c-ecc5-4fa4-bfdf-8c584f1a1332
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 85ccefaddf6e8f0bad35d3a01d1b355f0482db9c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="managing-backups-sybasetosql"></a>Gerenciando Backups (SybaseToSQL)
Gerenciamento de Backup do Sybase permite backup e restauração de dados da tabela antes ou depois de executar um teste. Você também pode gerenciar o conteúdo de backup com a caixa de diálogo Gerenciar conteúdos de Backup.  
  
## <a name="sybase-backup-management"></a>Gerenciamento de Backup do Sybase  
  
### <a name="backup"></a>Backup  
Para abrir a caixa de diálogo backup no Testador menu, aponte para o gerenciamento de Backup do Sybase, em seguida, clique em Backup... Na caixa de diálogo backup, você encontrará a árvore do Sybase Metadata exibindo todas as tabelas do esquema do Sybase carregado. Selecione uma ou mais tabelas para realizar um backup.  
  
Os botões a seguir estão disponíveis na caixa de diálogo:  
  
-   Clique o **verificar estado** botão para verificar o estado de backup da tabela.  
  
-   Clique o **Backup** botão para fazer backup da tabela de dados.  
  
-   Clique o **Cancelar** para fechar a caixa de diálogo.  
  
### <a name="restore"></a>Restaurar  
Para abrir a caixa de diálogo de restauração, no menu testador, aponte para gerenciamento de Backup do Sybase e clique em Restaurar... Lá você encontrará uma árvore que contém as tabelas disponíveis no backup. Selecione uma ou mais tabelas para restaurar seus dados.  
  
Os botões a seguir estão disponíveis na caixa de diálogo:  
  
-   Clique o **verificar estado** botão para verificar o estado de backup da tabela.  
  
-   Clique o **restaurar** botão para restaurar o backup de dados na tabela.  
  
-   Clique o **Cancelar** para fechar a caixa de diálogo.  
  
### <a name="managing-backup-contents"></a>Gerenciamento de conteúdo de Backup  
Para abrir o gerenciamento de conteúdo de Backup, no menu testador, aponte para o gerenciamento de Backup do Sybase e clique em conteúdo de Backup... Lá você encontrará uma árvore que contém as tabelas no backup.  
  
Os botões a seguir estão disponíveis na caixa de diálogo:  
  
-   Clique o **verificar estado** botão para verificar o estado de backup da tabela.  
  
-   Clique o **remover** botão para remover a tabela a partir do backup.  
  
-   Clique o **fechar** para fechar a caixa de diálogo.  
  
## <a name="sql-server-backup-management"></a>Gerenciamento de Backup do SQL Server  
Gerenciamento de Backup do SQL Server permite backup e restauração de dados da tabela antes ou depois de executar um teste. Você também pode gerenciar o conteúdo de backup com a caixa de diálogo Gerenciar conteúdos de Backup.  
  
### <a name="backup"></a>Backup  
Para abrir a caixa de diálogo backup no Testador menu, aponte para o gerenciamento de Backup do SQL Server, clique em Backup... Na caixa de diálogo backup, você encontrará a árvore de metadados do SQL Server exibe todas as tabelas dos bancos de dados do SQL Server carregados. Selecione uma ou mais tabelas para realizar um backup.  
  
Os botões a seguir estão disponíveis na caixa de diálogo:  
  
-   Clique o **verificar estado** botão para verificar o estado de backup da tabela.  
  
-   Clique o **Backup** botão para fazer backup dos dados da tabela.  
  
-   Clique o **Cancelar** para fechar a caixa de diálogo.  
  
### <a name="restore"></a>Restaurar  
Para abrir a caixa de diálogo de restauração, no menu testador, aponte para o gerenciamento de Backup do SQL Server, clique em Restaurar... Lá você encontrará uma árvore que contém as tabelas disponíveis no backup. Selecione um ou mais tabela para restaurar seus dados.  
  
Os botões a seguir estão disponíveis na caixa de diálogo:  
  
-   Clique o **verificar estado** botão para verificar o estado de backup da tabela.  
  
-   Clique o **restaurar** botão para restaurar o backup de dados na tabela.  
  
-   Clique o **Cancelar** para fechar a caixa de diálogo.  
  
### <a name="managing-backup-contents"></a>Gerenciamento de conteúdo de Backup  
Para abrir o gerenciamento de conteúdo de Backup, no menu testador, aponte para o gerenciamento de Backup do SQL Server e clique em conteúdo de Backup... Lá você encontrará uma árvore que contém as tabelas no backup.  
  
Os botões a seguir estão disponíveis na caixa de diálogo:  
  
-   Clique o **verificar estado** botão para verificar o estado de backup da tabela.  
  
-   Clique o **remover** botão para remover a tabela a partir do backup.  
  
-   Clique o **fechar** para fechar a caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
[Teste de objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
