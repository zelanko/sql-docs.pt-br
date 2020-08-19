---
description: Programa de instalação
title: Programa de instalação | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4cd4858214ff084a037002abd3bd34035160496b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421320"
---
# <a name="setup-program"></a>Programa de instalação
> **Observação:** A partir do Windows XP e do Windows Server 2003, **o ODBC está incluído no sistema operacional Windows**. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 O usuário executa o programa de instalação para iniciar o processo de instalação. O programa de instalação é escrito pelo desenvolvedor do aplicativo ou driver. Além de instalar componentes ODBC, ele pode instalar outro software. Por exemplo, os desenvolvedores de aplicativos podem usar o mesmo programa de instalação para instalar componentes ODBC e para instalar seus aplicativos.  
  
 Os desenvolvedores podem escrever o programa de instalação do zero, usando os utilitários de instalação do Microsoft® Windows® SDK ou o software de instalação de outros fornecedores. Isso dá aos desenvolvedores controle total sobre a aparência do programa de instalação. O programa de instalação pode ser escrito para instalar software adicional, como um aplicativo ODBC. Para obter mais informações sobre os utilitários de instalação do SDK do Windows, consulte a documentação do SDK do Windows.  
  
 A quantidade de instalação realmente feita pelo programa de instalação depende de quais funções ele chama na DLL do instalador. A DLL do instalador contém funções para instalar componentes individuais do ODBC. O programa de instalação simplesmente chama **SQLInstallDriverManager**, **SQLInstallDriverEx**ou **SQLInstallTranslatorEx** na DLL do instalador para recuperar o caminho do diretório no qual o componente deve ser instalado e adicionar informações sobre o componente ao registro. Essas funções não copiam arquivos de fato; o programa de instalação faz isso usando as informações nos argumentos dessas funções.  
  
 A DLL do instalador também contém funções para remover componentes ODBC. O programa de instalação chama **SQLRemoveDriverManager**, **SQLRemoveDriver**ou **SQLRemoveTranslator** na DLL do instalador para decrementar a contagem de uso de um componente no registro e, se a nova contagem de uso do componente for para 0, remova todas as informações sobre o componente do registro. Essas funções, na verdade, não removem os arquivos para o componente; o programa de instalação faz isso se a nova contagem de uso se enquadrar em 0.
