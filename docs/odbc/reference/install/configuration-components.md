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
manager: craigg
ms.openlocfilehash: bcf7d34f8faf70f57373ad1a5dae55261799145b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198413"
---
# <a name="configuration-components"></a>Componentes de configuração
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, ODBC está incluído no sistema operacional Windows. Você deve instalar apenas explicitamente ODBC em versões anteriores do Windows.  
  
 Fontes de dados são configuradas pelo instalador do DLL, que, por sua vez chama driver instalação DLLs e DLLs de instalação do tradutor conforme eles são necessários. O instalador do DLL é seja invocado diretamente no painel de controle ou carregado e chamado por outro programa, conhecido como o *programa de administração*. A ilustração a seguir mostra a relação entre os componentes de configuração.  
  
 ![Relação entre componentes de configuração](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 Para obter mais informações sobre esses componentes, consulte os tópicos a seguir no final desta seção.  
  
-   [Programa de instalação](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL do Instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalação do driver](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>Consulte também  
 [Componentes de instalação](../../../odbc/reference/install/installation-components.md)
