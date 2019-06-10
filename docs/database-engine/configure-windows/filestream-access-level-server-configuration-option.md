---
title: Opção de configuração de servidor filestream access level | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 81d5627c46f12a033de5dab881f2c6de7f99e2f4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66785326"
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
  
## <a name="see-also"></a>Consulte Também  
 [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](https://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [Habilitar e configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
