---
title: "Op&#231;&#227;o allow updates de configura&#231;&#227;o de Servidor | Microsoft Docs"
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
  - "opção allow updates"
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# Op&#231;&#227;o allow updates de configura&#231;&#227;o de Servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Essa opção ainda está presente no procedimento armazenado **sp_configure**, embora sua funcionalidade esteja indisponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A configuração não tem nenhum efeito. Não serão aceitas atualizações diretas para as tabelas do sistema.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 A alteração da opção **permitir atualizações** fará com que a instrução RECONFIGURE falhe. Alterações na opção **permitir atualizações** devem ser removidas de todos os scripts.  
  
## Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  