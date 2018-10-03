---
title: Componentes de instalação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 961ff9fe552fa30eaad4667fdd1911a44f3a35f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793034"
---
# <a name="installation-components"></a>Componentes de instalação
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, ODBC está incluído no sistema operacional Windows. Você deve instalar apenas explicitamente ODBC em versões anteriores do Windows.  
  
 O processo de instalação é iniciado quando o usuário executa o programa de instalação. O programa de instalação funciona em conjunto com o *DLL do instalador* e uma *DLL de instalação do driver* para cada driver. O programa de instalação e a DLL do instalador usam argumentos de **SQLInstallDriverEx** e **SQLInstallTranslatorEx** funções para determinar quais arquivos deseja copiar ou excluir para cada componente. A ilustração a seguir mostra a relação entre esses componentes de instalação.  
  
 ![Relação entre componentes de instalação](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]  
>  O arquivo Odbc.inf que foi usado no ODBC 2. *x* para descrever os arquivos necessários para cada ODBC componente não é usada em ODBC 3 *. x*. Drivers que são fornecidos ODBC 3 *. x* componentes não é necessário criar um arquivo Odbc.inf. A remoção de **SQLInstallDriver** e **SQLInstallODBC**e a substituição do **SQLInstallTranslator**, ter processado Odbc.inf desnecessários. As informações do driver que costumavam ser nas seções a palavra-chave Driver Odbc.inf agora são fornecidas na *lpszDriver* argumento **SQLInstallDriverEx**. As informações de tradução que costumava ser no [ODBC tradutor] e seções de especificação de tradução de Odbc.inf agora é fornecido na *lpszTranslator* argumento de **SQLInstallTranslatorEx**. Essas alterações permitem que o instalador ODBC seja mais portátil entre plataformas.  
  
 Para obter mais informações sobre esses componentes, consulte os tópicos a seguir no final desta seção.  
  
-   [Programa de instalação](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL do Instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalação do driver](../../../odbc/reference/install/driver-setup-dll.md)
