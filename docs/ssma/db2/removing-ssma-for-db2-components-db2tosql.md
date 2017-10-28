---
title: Removendo o SSMA para componentes de DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b26a45f1f8592de1650e3c7ee03c710ff8e3aea0
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>Removendo o SSMA para componentes de DB2 (DB2ToSQL)
Quando terminar de migrar bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], talvez você queira desinstalar componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, você deve desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , a menos que seus bancos de dados migrados não usam funções no **ssma_DB2** esquema do **sysdb** banco de dados.  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>Desinstalando o SSMA para cliente DB2  
Você pode desinstalar o SSMA usando **adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para DB2**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalar o pacote de extensão  
Se você tiver certeza de seus bancos de dados migrados não usam objetos de **sysdb.ssma_DB2** esquema, você pode excluí-lo do esquema para remover o pacote de extensão – há é sem desinstalar o Windows  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para DB2 cliente &#40; DB2ToSQL &#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[Instalando componentes do SSMA do SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  

