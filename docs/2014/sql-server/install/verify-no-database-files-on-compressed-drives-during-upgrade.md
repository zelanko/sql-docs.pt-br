---
title: Verificar se nenhum arquivo de banco de dados está em unidades compactadas durante o processo de atualização | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- compressed drives [SQL Server]
ms.assetid: 63be6853-c54a-42b2-ae1a-db2175f1d28e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9c04f7890ba8d8efe64afaf11b922af156c5de46
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065130"
---
# <a name="verify-that-no-database-files-are-on-compressed-drives-during-the-upgrade-process"></a>Verificar se não há arquivos de banco de dados em unidades compactadas durante o processo de atualização
  O Supervisor de Atualização detectou arquivos de banco de dados em uma unidade compactada. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode criar nem atualizar bancos de dados em unidades compactadas.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Ao instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione uma unidade não compactada para os bancos de dados do sistema e certifique-se de que os bancos de dados que serão atualizados não estão em unidades compactadas. Porém, saiba que depois que o banco de dados foi atualizado, você pode colocar bancos de dados somente leitura e grupos de arquivos secundários somente leitura em um sistema de arquivo compactado NTFS.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
