---
title: "Propriedades do banco de dados (página Grupos de Arquivos) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.databaseproperties.filegroups.f1
ms.assetid: 8d06e859-73dd-4019-b6e8-99c5c5297697
caps.latest.revision: "31"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5059c901a9b2dc517b765a642ddbe16bb926471
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="database-properties-filegroups-page"></a>Propriedades do banco de dados (página Grupos de Arquivos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use esta página para exibir os grupos de arquivos ou para adicionar um grupo de arquivos novo ao banco de dados selecionado. Os tipos de grupos de arquivos estão separados em grupos de arquivos *row* , dados FILESTREAM e grupos de arquivos com otimização de memória.  
  
 Os grupos de arquivos tipo linha contêm dados e arquivos de log normais. Os grupos de arquivos de dados FILESTREAM contêm arquivos de dados FILESTREAM. Esses arquivos de dados armazenam informações sobre como os dados de objetos binários grandes (BLOB) são salvos no sistema de arquivos quando usar o armazenamento FILESTREAM. As opções são as mesmas para os dois tipos de grupos de arquivos.  
  
 Se o FILESTREAM não estiver habilitado, a seção **Fluxo de arquivos** não estará disponível. Você pode habilitar o armazenamento FILESTREAM usando as [Propriedades do Servidor (Página Avançada)](../../database-engine/configure-windows/server-properties-advanced-page.md).  
  
 Para obter informações sobre como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa grupos de arquivos linha, veja [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md). Para obter mais informações sobre os dados de FILESTREAM e os grupos de arquivos, veja [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 Os grupos de arquivos com otimização de memória são necessários para um banco de dados conter uma ou mais tabelas com otimização de memória.  
  
## <a name="row-and-filestream-data-filegroup-options"></a>Opções de grupo de arquivos de dados de linha e FILESTREAM  
 **Nome**  
 Digite o nome do grupo de arquivos.  
  
 **Arquivos**  
 Exibe a contagem dos arquivos no grupo de arquivos.  
  
 **Somente leitura**  
 Selecione para definir o grupo de arquivos com o status de somente leitura.  
  
 **Default**  
 Selecione para tornar este grupo de arquivos o grupo de arquivos padrão. Você pode ter um grupo de arquivos padrão para linha e outro para os dados do FILESTREAM.  
  
 **Adicionar**  
 Adiciona uma nova linha em branco aos grupos de arquivos da listagem de grade do banco de dados.  
  
 **Remover**  
 Remove da grade a linha do grupo de arquivos selecionada.  
  
## <a name="memory-optimized-data-filegroup-options"></a>Opções de grupo de arquivos de dados com otimização de memória  
 **Nome**  
 Digite o nome do grupo de arquivos com otimização de memória.  
  
 **Arquivos Filestream**  
 Exibe o número de arquivos (contêineres) no grupo de arquivos de dados com otimização de memória. Você pode adicionar contêineres na página **Arquivos** .  
  
 **Adicionar**  
 Adiciona uma nova linha em branco aos grupos de arquivos da listagem de grade do banco de dados.  
  
 **Remover**  
 Remove da grade a linha do grupo de arquivos selecionada.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  
