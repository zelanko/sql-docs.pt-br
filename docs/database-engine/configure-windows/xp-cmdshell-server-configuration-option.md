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
ms.openlocfilehash: b2d4364d01b871364fda3ac42d98536e99269c29
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85763951"
---
# <a name="xp_cmdshell-server-configuration-option"></a>Opção de configuração do servidor xp_cmdshell

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo descreve como habilitar a opção de configuração **xp_cmdshell** do SQL Server. Essa opção permite que os administradores do sistema controlem se o [procedimento armazenado estendido xp_cmdshell](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md) pode ser executado em um sistema. Por padrão, a opção **xp_cmdshell** é desabilitada em novas instalações.

Antes de habilitar essa opção, é importante considerar as possíveis implicações de segurança.

- O código desenvolvido recentemente não deve usar o procedimento armazenado **xp_cmdshell** e, em geral, ele deve ser mantido desabilitado.
- Alguns aplicativos herdados exigem que o **xp_cmdshell** seja habilitado. Se eles não puderem ser modificados para evitar o uso desse procedimento armazenado, habilite-o conforme descrito abaixo.

Se precisar habilitar o **xp_cmdshell**, use o [Gerenciamento baseado em políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md) ou execute o procedimento armazenado do sistema **sp_configure**, conforme mostrado no seguinte exemplo de código:  
  
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
