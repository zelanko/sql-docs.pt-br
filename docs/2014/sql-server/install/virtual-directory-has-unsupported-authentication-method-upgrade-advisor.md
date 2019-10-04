---
title: O diretório virtual tem um método de autenticação sem suporte (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 216eca6f-9a66-42e1-aa54-dcf99cec9f7d
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 26420df466860677f22d39d57133568a2f02bc68
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952015"
---
# <a name="virtual-directory-has-unsupported-authentication-method-upgrade-advisor"></a>Diretório virtual com método de autenticação sem suporte (Supervisor de Atualização)
  O Supervisor de Atualização detectou um método de autenticação sem suporte no diretório virtual do Gerenciador de Relatórios ou do servidor de relatório. Os métodos de autenticação para os quais a atualização não oferece suporte incluem Anônimo, Digest e .NET Passport.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 A instalação não pode atualizar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que use um dos métodos de autenticação a seguir  
  
-   Anônima  
  
-   Digest  
  
-   .NET Passport  
  
 Para continuar, você pode modificar o método de autenticação especificado para os diretórios virtuais do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no Internet Information Services (IIS) ou migrar sua instalação. Para obter mais informações sobre como migrar sua instalação, consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para continuar com atualização, modifique o método de autenticação do IIS dos diretórios virtuais do ReportServer e Reports. Para obter mais informações sobre como modificar os métodos de autenticação no IIS, consulte a documentação do IIS. Depois que você modificar o método de autenticação dos diretórios virtuais do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], execute novamente o Supervisor de Atualização para confirmar que não existe nenhum outro problema de atualização.  
  
## <a name="see-also"></a>Consulte também  
 [Supervisor de atualização &#40;de problemas de atualização do Reporting Services&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
