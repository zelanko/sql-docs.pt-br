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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a196e9b935229fa03c6dd0eda92b8e99e69f0ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285246"
---
# <a name="installation-components"></a>Componentes de instalação
> [!NOTE]  
>  Começando com o Windows XP e o Windows Server 2003, o ODBC está incluído no sistema operacional windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 O processo de instalação começa quando o usuário executa o programa de configuração. O programa de configuração funciona em conjunto com o *instalador DLL* e uma *DLL de configuração do driver* para cada driver. Tanto o programa de configuração quanto o instalador DLL usam os argumentos nas funções **SQLInstallDriverEx** e **SQLInstallTranslatorEx** para determinar quais arquivos copiar ou excluir para cada componente. A ilustração a seguir mostra a relação entre esses componentes de instalação.  
  
 ![Relação entre componentes de instalação](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  O arquivo Odbc.inf que foi usado no ODBC *2.x* para descrever os arquivos exigidos por cada componente ODBC não é usado no ODBC *3.x*. Os drivers que enviam componentes ODBC *3.x* não precisam criar um arquivo Odbc.inf. A remoção do **SQLInstallDriver** e **do SQLInstallODBC**e a depreciação do **SQLInstallTranslator**tornaram o Odbc.inf desnecessário. As informações do driver que costumavam estar nas seções Driver Keyword do Odbc.inf agora são fornecidas no argumento *lpszDriver* no **SQLInstallDriverEx**. As informações do tradutor que costumavam estar nas seções [Tradutor oDBC] e Especificação do Tradutor do Odbc.inf agora são fornecidas no argumento *lpszTranslator* do **SQLInstallTranslatorEx**. Essas alterações permitem que o Instalador ODBC seja mais portátil entre as plataformas.  
  
 Para obter mais informações sobre esses componentes, consulte os seguintes tópicos no final desta seção.  
  
-   [Programa de instalação](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL do Instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalação do driver](../../../odbc/reference/install/driver-setup-dll.md)
