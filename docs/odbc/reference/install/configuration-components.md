---
title: Componentes de configuração | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], configuring
ms.assetid: 0b68ff48-12e4-41aa-b9e2-b39ed5023ea7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37c2518c3b18423c804631780ee4a18bff29d88b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289007"
---
# <a name="configuration-components"></a>Componentes de configuração
> [!NOTE]  
>  Começando com o Windows XP e o Windows Server 2003, o ODBC está incluído no sistema operacional windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 As fontes de dados são configuradas pelo instalador DLL, que por sua vez chama dLLs de configuração de driver e DLLs de configuração de tradutor conforme necessário. O instalador DLL é invocado diretamente do Painel de Controle ou carregado e chamado por outro programa, conhecido como *programa de administração*. A ilustração a seguir mostra a relação entre os componentes de configuração.  
  
 ![Relação entre componentes de configuração](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 Para obter mais informações sobre esses componentes, consulte os seguintes tópicos no final desta seção.  
  
-   [Programa de instalação](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL do Instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalação do driver](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Componentes de instalação](../../../odbc/reference/install/installation-components.md)
