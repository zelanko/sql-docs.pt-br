---
title: Segurança e proteção do Reporting Services | Microsoft Docs
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 189c0d314ba3f16b00ad570b3e0f9fbce9fa2f7e
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632413"
---
# <a name="reporting-services-security-and-protection"></a>Segurança e proteção do Reporting Services
  Você pode usar as informações desta seção para obter informações sobre os recursos de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta seção também explica os modelos de autorização e os provedores de autenticação com suporte no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="extended-protection-for-authentication"></a>Proteção Estendida para Autenticação  
 A partir do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], o suporte para Proteção Estendida para Autenticação está disponível. O recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte ao uso de associação de canal e associação de serviço para aprimorar a proteção da autenticação. Os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisam ser usados com um sistema operacional que ofereça suporte à Proteção Estendida. Para obter mais informações, consulte [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
## <a name="authentication-and-authorization"></a>Autenticação e autorização  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece diferentes tipos de autenticação para aplicativos de usuários e de cliente para autenticação com o servidor de relatório. O uso do tipo certo de autenticação para seu servidor de relatório permite obter o nível adequado de segurança necessário para sua organização. Para obter mais informações, consulte [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md).  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também utiliza funções e permissões para controlar o acesso de usuários ao conteúdo do catálogo do servidor de relatório (em outras palavras, quem pode acessar o que e como o acesso pode ser feito). Para obter mais informações, consulte [Funções e permissões &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrições das tarefas|Links|  
|-----------------------|-----------|  
|Configure o protocolo TLS, anteriormente conhecido como protocolo SSL (Secure Sockets Layer), para proteger as conexões de cliente com o servidor de relatório.|[Configurar conexões TLS em um servidor de relatório no modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  
