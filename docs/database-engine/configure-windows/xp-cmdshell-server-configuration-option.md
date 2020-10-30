---
title: Opção de configuração do servidor xp_cmdshell
description: Saiba mais sobre a opção "xp_cmdshell". Veja como ele controla se SQL Server pode executar o procedimento armazenado estendido "xp_cmdshell". Descubra como ativá-la.
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
author: markingmyname
ms.author: maghan
ms.custom: contperfq4
ms.date: 06/12/2020
ms.openlocfilehash: 004a7b0a50a657632bb2b9970f0558857d416494
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257974"
---
# <a name="xp_cmdshell-server-configuration-option"></a>Opção de configuração do servidor xp_cmdshell

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo descreve como habilitar a opção de configuração **xp_cmdshell** do SQL Server. Essa opção permite que os administradores do sistema controlem se o [procedimento armazenado estendido xp_cmdshell](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md) pode ser executado em um sistema. Por padrão, a opção **xp_cmdshell** é desabilitada em novas instalações.

Antes de habilitar essa opção, é importante considerar as possíveis implicações de segurança.

- O código desenvolvido recentemente não deve usar o procedimento armazenado **xp_cmdshell** e, em geral, ele deve ser mantido desabilitado.
- Alguns aplicativos herdados exigem que o **xp_cmdshell** seja habilitado. Se eles não puderem ser modificados para evitar o uso desse procedimento armazenado, habilite-o conforme descrito abaixo.

> [!NOTE]  
> Se **xp_cmdshell** precisar ser usado, como uma melhor prática de segurança, é recomendável habilitá-lo apenas durante a tarefa real que o exige.

Se precisar habilitar o **xp_cmdshell** , use o [Gerenciamento baseado em políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md) ou execute o procedimento armazenado do sistema **sp_configure** , conforme mostrado no seguinte exemplo de código:  
  
``` sql
-- To allow advanced options to be changed.  
EXECUTE sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXECUTE sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="next-steps"></a>Próximas etapas

- [Procedimento armazenado estendido xp_cmdshell](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)
- [Opções de configuração do servidor (SQL Server)](server-configuration-options-sql-server.md)
- [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
