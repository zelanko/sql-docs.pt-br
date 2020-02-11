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
ms.openlocfilehash: 34d1b6d143f6f40d73e2feeb0b718f3c3b3248fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094131"
---
# <a name="installation-components"></a>Componentes de instalação
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 O processo de instalação é iniciado quando o usuário executa o programa de instalação. O programa de instalação funciona em conjunto com a *dll do instalador* e uma DLL de instalação de *Driver* para cada driver. O programa de instalação e a DLL do instalador usam os argumentos nas funções **SQLInstallDriverEx** e **SQLInstallTranslatorEx** para determinar quais arquivos copiar ou excluir para cada componente. A ilustração a seguir mostra a relação entre esses componentes de instalação.  
  
 ![Relação entre componentes de instalação](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  O arquivo ODBC. inf que foi usado no ODBC *2. x* para descrever os arquivos exigidos por cada componente ODBC não é usado no ODBC *3. x*. Os drivers que enviam componentes ODBC *3. x* não precisam criar um arquivo ODBC. inf. A remoção de **SQLInstallDriver** e **SQLInstallODBC**, e a substituição de **SQLInstallTranslator**, fez com que o ODBC. inf fosse desnecessário. As informações de driver que costumava estar nas seções de palavra-chave do driver de ODBC. inf agora são fornecidas no argumento *lpszDriver* em **SQLInstallDriverEx**. As informações do tradutor que costumava estar no [conversor ODBC] e nas seções de especificação do tradutor de ODBC. inf agora são fornecidas no argumento *lpszTranslator* de **SQLInstallTranslatorEx**. Essas alterações permitem que o ODBC Installer seja mais portável entre plataformas.  
  
 Para obter mais informações sobre esses componentes, consulte os tópicos a seguir no final desta seção.  
  
-   [Programa de instalação](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL do Instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalação do driver](../../../odbc/reference/install/driver-setup-dll.md)
