---
title: "Op&#231;&#227;o de configura&#231;&#227;o de servidor filestream access level | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FILESTREAM [SQL Server], nível de acesso"
  - "nível de acesso de fluxo de arquivos"
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# Op&#231;&#227;o de configura&#231;&#227;o de servidor filestream access level
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Use a opção filestream_access_level para alterar o nível de acesso de FILESTREAM dessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para que essa opção surta efeito, as configurações de administração do Windows para FILESTREAM devem ser habilitadas. Você pode habilitar essas configurações ao instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usando o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Valor|Definição|  
|-----------|----------------|  
|0|Desabilita o suporte a FILESTREAM para esta instância.|  
|1|Habilita FILESTREAM para o acesso a [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|2|Habilita FILESTREAM para acesso de fluxo de [!INCLUDE[tsql](../../includes/tsql-md.md)] e Win32|  
  
## Consulte também  
 [Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos](../Topic/Database%20Engine%20Configuration%20-%20Filestream.md)   
 [Habilitar e configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  