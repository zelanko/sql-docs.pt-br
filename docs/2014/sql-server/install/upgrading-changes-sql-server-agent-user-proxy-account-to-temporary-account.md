---
title: Atualização mudará a conta de Proxy de usuário do SQL Server Agent para UpgradedProxyAccount temporária | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
ms.assetid: cd2d08c3-4e56-4034-8b68-0c78df8b5471
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a82cbcc9ef1ab57279b44cc83509cb1efad855ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091397"
---
# <a name="upgrading-will-change-the-sql-server-agent-user-proxy-account-to-the-temporary-upgradedproxyaccount"></a>Atualização mudará a Conta Proxy do Usuário do SQL Server Agent para o UpgradedProxyAccount temporário
  Planos de manutenção de banco de dados que têm envio de log habilitado não serão ativados após a atualização.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>Descrição  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um conjunto novo de funções de envio de log que não são diretamente compatíveis com planos de manutenção do banco de dados.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Usuários do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] que possuem planos de manutenção do banco de dados com funções de envio de log devem configurar o envio de log usando as novas funções. Para obter mais informações, pesquise sobre 'envio de log’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [A categoria de trabalho de envio de log do SQL Server Agent causa falha na atualização](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [Envio de log não executará após a atualização](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)  
  
  
