---
title: Remover o SSMA para componentes do DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 25c8222009c2ea9358c0bab2ad5ae077588fb3cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060090"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>Remover o SSMA para componentes do DB2 (DB2ToSQL)
Quando você terminar de migrar bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], talvez você queira desinstalar os componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, você não deve desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que seus bancos de dados migrados não usam funções na **ssma_DB2** esquema dos **sysdb** banco de dados.  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>Desinstalando o SSMA para cliente DB2  
Você pode desinstalar o SSMA usando **adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para o DB2**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando o pacote de extensão  
Se você tiver certeza seus bancos de dados migrados não usam objetos de **sysdb.ssma_DB2** esquema, você pode remover o pacote de extensão, excluindo-o do esquema - não há é nenhuma desinstalação do Windows  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para cliente DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[Instalar os componentes do SSMA no SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
