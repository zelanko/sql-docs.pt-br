---
title: Opção de configuração de servidor allow updates | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a9acdfa9668a49ed5e0c67a932bacc1ccee1ac6b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196106"
---
# <a name="allow-updates-server-configuration-option"></a>Opção allow updates de configuração de Servidor
  Essa opção ainda está presente no procedimento armazenado **sp_configure** , embora sua funcionalidade esteja indisponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A configuração não tem nenhum efeito. Não serão aceitas atualizações diretas para as tabelas do sistema.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 A alteração da opção **permitir atualizações** fará com que a instrução RECONFIGURE falhe. Alterações na opção **permitir atualizações** devem ser removidas de todos os scripts.  
  
## <a name="see-also"></a>Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
