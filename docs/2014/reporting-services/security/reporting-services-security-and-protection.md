---
title: Segurança e proteção do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0f8c7a4186c5236260fb27d8de107ce8c97bd363
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101968"
---
# <a name="reporting-services-security-and-protection"></a>Segurança e proteção do Reporting Services
  Você pode usar as informações desta seção para obter informações sobre os recursos de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta seção também explica os modelos de autorização e os provedores de autenticação com suporte no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="extended-protection-for-authentication"></a>Proteção Estendida para Autenticação  
 A partir do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], o suporte para Proteção Estendida para Autenticação está disponível. O recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte ao uso de associação de canal e associação de serviço para aprimorar a proteção da autenticação. Os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisam ser usados com um sistema operacional que ofereça suporte à Proteção Estendida. Para obter mais informações, consulte [Extended Protection for Authentication with Reporting Services](extended-protection-for-authentication-with-reporting-services.md).  
  
## <a name="authentication-and-authorization"></a>Autenticação e autorização  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece diferentes tipos de autenticação para aplicativos de usuários e de cliente para autenticação com o servidor de relatório. O uso do tipo certo de autenticação para seu servidor de relatório permite obter o nível adequado de segurança necessário para sua organização. Para obter mais informações, consulte [Authentication with the Report Server](authentication-with-the-report-server.md).  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também utiliza funções e permissões para controlar o acesso de usuários ao conteúdo do catálogo do servidor de relatório (em outras palavras, quem pode acessar o que e como o acesso pode ser feito). Para obter mais informações, consulte [Funções e permissões &#40;Reporting Services&#41;](roles-and-permissions-reporting-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrições das tarefas|Links|  
|-----------------------|-----------|  
|Configurar o protocolo SSL para proteger conexões de cliente com o servidor de relatório.|[Configurar conexões SSL em um servidor de relatórios de Modo Nativo](configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  
