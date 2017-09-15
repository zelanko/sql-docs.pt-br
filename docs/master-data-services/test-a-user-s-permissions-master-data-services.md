---
title: "Testar permissões de um usuário (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
caps.latest.revision: 4
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 6e3a240837692dbe8ea3cdfdcba42035e0317e78
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="test-a-user39s-permissions-master-data-services"></a>Testar permissões de um usuário (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode criar um usuário de teste e registrar em log no aplicativo Web para testar permissions. Quando um usuário tenta acessar a URL [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , as credenciais do usuário são autenticadas. No Internet Explorer, as configurações de segurança controlam se isso ocorre automaticamente ou se o usuário deve inserir nome de usuário e senha. Para alterar essas configurações, conclua as seguintes etapas:  
  
### <a name="to-test-a-users-security"></a>Para testar a segurança de um usuário  
  
1.  No Internet Explorer 7 e posterior, clique em **Ferramentas**, em **Opções de Internet**e na guia **Segurança** .  
  
2.  Clique em **Intranet Local** e no botão **Nível Personalizado** .  
  
3.  Na seção **Autenticação de Usuário** , escolha **Aviso para nome de usuário e senha**.  
  
4.  Da próxima vez que você abrir a janela do navegador, será solicitado a fornecer um nome de usuário e senha.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
