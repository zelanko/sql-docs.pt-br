---
title: Opção de configuração de servidor Ole Automation Procedures | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f00c238dfb32089261c51936b3937b0657c58b08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782024"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Opção de configuração de servidor Ole Automation Procedures
  Use a opção `Ole Automation Procedures` para especificar se podem ser instanciados objetos de automação OLE dentro de lotes [!INCLUDE[tsql](../../includes/tsql-md.md)]. Essa opção também pode ser configurada com o Gerenciamento Baseado em Políticas ou o procedimento armazenado **sp_configure** . Para obter mais informações, consulte [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
 A opção `Ole Automation Procedures` pode ser definida com os valores a seguir.  
  
 0  
 Os procedimentos de automação OLE estão desabilitados. Padrão para novas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 1  
 Os procedimentos de automação OLE estão habilitados.  
  
 Quando os Procedimentos da Automação OLE forem habilitados, uma chamada a **sp_OACreate** fará com que se inicie o ambiente OLE de execução compartilhado.  
  
 O valor atual do `Ole Automation Procedures` opção pode ser exibida e alterada usando o **sp_configure** procedimento armazenado do sistema.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
