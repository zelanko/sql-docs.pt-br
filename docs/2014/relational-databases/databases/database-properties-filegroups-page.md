---
title: Propriedades do banco de dados (página Grupos de Arquivos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.filegroups.f1
ms.assetid: 8d06e859-73dd-4019-b6e8-99c5c5297697
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b8de45556d3c19ee8460b33e7f07ceb485b37597
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917102"
---
# <a name="database-properties-filegroups-page"></a>Propriedades do banco de dados (página Grupos de Arquivos)
  Use esta página para exibir os grupos de arquivos ou para adicionar um grupo de arquivos novo ao banco de dados selecionado. Os tipos de grupos de arquivos estão separados em grupos de arquivos *row* , dados FILESTREAM e grupos de arquivos com otimização de memória.  
  
 Os grupos de arquivos tipo linha contêm dados e arquivos de log normais. Os grupos de arquivos de dados FILESTREAM contêm arquivos de dados FILESTREAM. Esses arquivos de dados armazenam informações sobre como os dados de objetos binários grandes (BLOB) são salvos no sistema de arquivos quando usar o armazenamento FILESTREAM. As opções são as mesmas para os dois tipos de grupos de arquivos.  
  
 Se o FILESTREAM não estiver habilitado, a seção **Fluxo de arquivos** não estará disponível. Você pode habilitar o armazenamento FILESTREAM usando as [Propriedades do Servidor (Página Avançada)](../../database-engine/configure-windows/server-properties-advanced-page.md).  
  
 Para obter informações sobre como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa grupos de arquivos linha, veja [Arquivos e grupos de arquivos do banco de dados](database-files-and-filegroups.md). Para obter mais informações sobre os dados de FILESTREAM e os grupos de arquivos, veja [FILESTREAM &#40;SQL Server&#41;](../blob/filestream-sql-server.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
