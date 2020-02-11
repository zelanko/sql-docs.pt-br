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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 248a9e31b176444ad51cb3a62c7c5f12f1b7bde3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068581"
---
# <a name="configuration-components"></a>Componentes de configuração
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 As fontes de dados são configuradas pela DLL do instalador que, por sua vez, chama DLLs de instalação de driver e DLLs de instalação do tradutor conforme necessário. A DLL do instalador é invocada diretamente do painel de controle ou carregada e chamada por outro programa, conhecida como *programa de administração*. A ilustração a seguir mostra a relação entre os componentes de configuração.  
  
 ![Relação entre componentes de configuração](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 Para obter mais informações sobre esses componentes, consulte os tópicos a seguir no final desta seção.  
  
-   [Programa de instalação](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL do Instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalação do driver](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Componentes de instalação](../../../odbc/reference/install/installation-components.md)
