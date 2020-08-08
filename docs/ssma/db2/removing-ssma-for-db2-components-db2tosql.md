---
title: Removendo os componentes do SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6e5d1cd88027dfa3fb4216c93ab4e660ddcc0dc9
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936630"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>Removendo o SSMA para DB2ToSQL (componentes do DB2)
Quando terminar de migrar bancos de dados do DB2 para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , talvez você queira desinstalar os componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, você não deve desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que os bancos de dados migrados não usem mais funções no esquema de **ssma_DB2** do **sysdb** .  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>Desinstalando o cliente SSMA para DB2  
Você pode desinstalar o SSMA usando **Adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No Painel de Controle, abra **Adicionar ou Remover Programas**.  
  
2.  Selecione ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para DB2**e clique em **remover**.  
  
3.  Para confirmar que deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando o pacote de extensão  
Se você tiver certeza de que seus bancos de dados migrados não usam objetos no esquema **sysdb. ssma_DB2** , você pode remover o pacote de extensão excluindo-o do esquema-não há nenhuma desinstalação do Windows  
  
## <a name="see-also"></a>Consulte Também  
[Instalação do SSMA para cliente DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[Instalando os componentes do SSMA em SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
