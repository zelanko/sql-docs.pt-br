---
title: Opção de configuração de servidor filestream access level | Microsoft Docs
description: Familiarize-se com a opção "filestream_access_level". Veja como ela altera o nível de acesso FILESTREAM para uma instância do SQL Server.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b891ba283acb1176a60bcc64105e126192aa8225
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772453"
---
# <a name="filestream-access-level-server-configuration-option"></a>Opção de configuração de servidor filestream access level
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Use a opção filestream_access_level para alterar o nível de acesso de FILESTREAM dessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para que essa opção surta efeito, as configurações de administração do Windows para FILESTREAM devem ser habilitadas. Você pode habilitar essas configurações ao instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usando o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Valor|Definição|  
|-----------|----------------|  
|0|Desabilita o suporte a FILESTREAM para esta instância.|  
|1|Habilita FILESTREAM para o acesso a [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|2|Habilita FILESTREAM para acesso de fluxo de [!INCLUDE[tsql](../../includes/tsql-md.md)] e Win32|  
  
## <a name="see-also"></a>Consulte Também  
 [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](https://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [Habilitar e configurar o FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
