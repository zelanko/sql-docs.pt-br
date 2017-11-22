---
title: "Opção de configuração de servidor filestream access level | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82c17104c43118a62fe3ca1c87db97479bffee4e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="filestream-access-level-server-configuration-option"></a>Opção de configuração de servidor filestream access level
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção filestream_access_level para alterar o nível de acesso de FILESTREAM dessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para que essa opção surta efeito, as configurações de administração do Windows para FILESTREAM devem ser habilitadas. Você pode habilitar essas configurações ao instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usando o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Valor|Definição|  
|-----------|----------------|  
|0|Desabilita o suporte a FILESTREAM para esta instância.|  
|1|Habilita FILESTREAM para o acesso a [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|2|Habilita FILESTREAM para acesso de fluxo de [!INCLUDE[tsql](../../includes/tsql-md.md)] e Win32|  
  
## <a name="see-also"></a>Consulte também  
 [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](http://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [Habilitar e configurar o FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
