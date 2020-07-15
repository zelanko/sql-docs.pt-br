---
title: Opção de configuração de servidor Ole Automation Procedures | Microsoft Docs
description: Saiba mais sobre a opção "Ole Automation Procedures". Veja como ela especifica se o SQL Server pode instanciar objetos de Automação OLE dentro de lotes Transact-SQL.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5390fce7517b56ea26a33392a72da7cb39dcd34d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773678"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Opção de configuração de servidor Ole Automation Procedures
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Use a opção **Procedimentos da Automação OLE** para especificar se podem ser instanciados objetos de automação OLE nos lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] . Essa opção também pode ser configurada com o Gerenciamento Baseado em Políticas ou o procedimento armazenado **sp_configure** . Para obter mais informações, consulte [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
 A opção **Ole Automation Procedures** pode ser definida com os valores a seguir.  
  
 0  
 Os procedimentos de automação OLE estão desabilitados. Padrão para novas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 1  
 Os procedimentos de automação OLE estão habilitados.  
  
 Quando os Procedimentos da Automação OLE forem habilitados, uma chamada a **sp_OACreate** fará com que se inicie o ambiente OLE de execução compartilhado.  
  
 O valor atual da opção **Procedimentos da Automação OLE** pode ser exibido e alterado por meio do procedimento armazenado do sistema **sp_configure** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como exibir a configuração atual dos procedimentos de automação OLE.  
  
```  
EXEC sp_configure 'Ole Automation Procedures';  
GO  
```  
  
 O exemplo a seguir mostra como habilitar os procedimentos de automação OLE.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Ole Automation Procedures', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Configuração da Área de Superfície](../../relational-databases/security/surface-area-configuration.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
