---
title: Atualização mudará a conta de Proxy de usuário do SQL Server Agent para a UpgradedProxyAccount temporária | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log shipping [SQL Server Agent]
ms.assetid: cd2d08c3-4e56-4034-8b68-0c78df8b5471
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9bae867b97a9fc63b97506fd8900e68b670b8013
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006743"
---
# <a name="upgrading-will-change-the-sql-server-agent-user-proxy-account-to-the-temporary-upgradedproxyaccount"></a>Atualização mudará a Conta Proxy do Usuário do SQL Server Agent para o UpgradedProxyAccount temporário
  Planos de manutenção de banco de dados que têm envio de log habilitado não serão ativados após a atualização.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>Description  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um conjunto novo de funções de envio de log que não são diretamente compatíveis com planos de manutenção do banco de dados.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Usuários do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] que possuem planos de manutenção do banco de dados com funções de envio de log devem configurar o envio de log usando as novas funções. Para obter mais informações, pesquise sobre 'envio de log’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de trabalho envio de log do SQL Server Agent causa falha na atualização](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [O envio de log não será executado após a atualização](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)  
  
  