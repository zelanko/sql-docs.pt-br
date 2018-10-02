---
title: Opção de configuração de servidor allow updates | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e27491d0f0c45660b736bcb01b993065941490f6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646681"
---
# <a name="allow-updates-server-configuration-option"></a>Opção allow updates de configuração de Servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Essa opção ainda está presente no procedimento armazenado **sp_configure** , embora sua funcionalidade esteja indisponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A configuração não tem nenhum efeito. Não serão aceitas atualizações diretas para as tabelas do sistema.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 A alteração da opção **permitir atualizações** fará com que a instrução RECONFIGURE falhe. Alterações na opção **permitir atualizações** devem ser removidas de todos os scripts.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
