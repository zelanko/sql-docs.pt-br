---
title: Opção de configuração de servidor allow updates | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d7e3ede317509a2044be90635db46e30a932af66
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935907"
---
# <a name="allow-updates-server-configuration-option"></a>Opção allow updates de configuração de Servidor
  Essa opção ainda está presente no procedimento armazenado **sp_configure** , embora sua funcionalidade esteja indisponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A configuração não tem nenhum efeito. Não serão aceitas atualizações diretas para as tabelas do sistema.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 A alteração da opção **permitir atualizações** fará com que a instrução RECONFIGURE falhe. Alterações na opção **permitir atualizações** devem ser removidas de todos os scripts.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
