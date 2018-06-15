---
title: Componentes de instalação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c5fe2538d1567630121f05a4798583099de7200
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917201"
---
# <a name="installation-components"></a>Componentes de instalação
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 O processo de instalação inicia quando o usuário executa o programa de instalação. O programa de instalação funciona em conjunto com o *instalador DLL* e um *DLL de instalação do driver* para cada driver. O programa de instalação e o instalador DLL usam os argumentos a **SQLInstallDriverEx** e **SQLInstallTranslatorEx** funções para determinar quais arquivos para copiar ou excluir para cada componente. A ilustração a seguir mostra a relação entre esses componentes de instalação.  
  
 ![Relação entre componentes de instalação](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]  
>  O arquivo Odbc.inf que foi usado no ODBC 2. *x* para descrever os arquivos necessários para cada ODBC o componente não é usada em ODBC 3 *. x*. Drivers que acompanham o ODBC 3 *. x* componentes não precisa criar um arquivo Odbc.inf. A remoção de **SQLInstallDriver** e **SQLInstallODBC**e a substituição de **SQLInstallTranslator**, tiver renderizado Odbc.inf desnecessários. As informações do driver que costumava ser nas seções a palavra-chave Driver Odbc.inf agora são fornecidas no *lpszDriver* argumento **SQLInstallDriverEx**. As informações de conversor que costumava ser no [ODBC tradutor] e seções de especificação de conversor de Odbc.inf agora é fornecida no *lpszTranslator* argumento de **SQLInstallTranslatorEx**. Essas alterações permitem que o instalador do ODBC ser mais portáteis entre plataformas.  
  
 Para obter mais informações sobre esses componentes, consulte os tópicos a seguir no final desta seção.  
  
-   [Programa de instalação](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL do Instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalação do driver](../../../odbc/reference/install/driver-setup-dll.md)
