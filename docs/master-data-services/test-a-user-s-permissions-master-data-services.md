---
title: Testar permissões de um usuário (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 38d4b1e7f9bd3e76c00bb4228e53e09416ed8557
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488097"
---
# <a name="test-a-user39s-permissions-master-data-services"></a>Testar permissões de um usuário (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode criar um usuário de teste e registrar em log no aplicativo Web para testar permissions. Quando um usuário tenta acessar a URL [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , as credenciais do usuário são autenticadas. No Internet Explorer, as configurações de segurança controlam se isso ocorre automaticamente ou se o usuário deve inserir nome de usuário e senha. Para alterar essas configurações, conclua as seguintes etapas:  
  
### <a name="to-test-a-users-security"></a>Para testar a segurança de um usuário  
  
1.  No Internet Explorer 7 e posterior, clique em **Ferramentas**, em **Opções de Internet**e na guia **Segurança** .  
  
2.  Clique em **Intranet Local** e no botão **Nível Personalizado** .  
  
3.  Na seção **Autenticação de Usuário** , escolha **Aviso para nome de usuário e senha**.  
  
4.  Da próxima vez que você abrir a janela do navegador, será solicitado a fornecer um nome de usuário e senha.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
