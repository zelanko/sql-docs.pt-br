---
title: Removendo os componentes do SSMA para DB2 (DB2ToSQL) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68060090"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>Removendo o SSMA para DB2ToSQL (componentes do DB2)
Quando terminar de migrar bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o, talvez você queira desinstalar os componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, você não deve desinstalar o pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de extensão de, a menos que os bancos de dados migrados não usem mais funções no esquema de **ssma_DB2** do **sysdb** .  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>Desinstalando o cliente SSMA para DB2  
Você pode desinstalar o SSMA usando **Adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No Painel de Controle, abra **Adicionar ou Remover Programas**.  
  
2.  ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] Selecione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assistente de migração para DB2**e clique em **remover**.  
  
3.  Para confirmar que deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando o pacote de extensão  
Se você tiver certeza de que seus bancos de dados migrados não usam objetos no esquema **sysdb. ssma_DB2** , você pode remover o pacote de extensão excluindo-o do esquema-não há nenhuma desinstalação do Windows  
  
## <a name="see-also"></a>Consulte Também  
[Instalação do SSMA para cliente DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[Instalando os componentes do SSMA em SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
