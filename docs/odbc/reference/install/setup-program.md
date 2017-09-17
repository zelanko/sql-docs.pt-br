---
title: "Programa de instalação | Microsoft Docs"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 30637bacfb73d56528233ea13c4c6daeabecf814
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setup-program"></a>Programa de instalação
> **Observação:** começando com o Windows XP e Windows Server 2003, **ODBC está incluído no sistema operacional Windows**. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 O usuário executa o programa de instalação para iniciar o processo de instalação. O programa de instalação é gravado pelo desenvolvedor do aplicativo ou driver. Além de instalar os componentes ODBC, ele poderá instalar outro software. Por exemplo, os desenvolvedores de aplicativos podem usar o mesmo programa de instalação para instalar os componentes ODBC e instalar seus aplicativos.  
  
 Os desenvolvedores podem gravar o programa de instalação do zero, usando o software de instalação de outros fornecedores ou utilitários de instalação do SDK do Microsoft® Windows®. Isso fornece aos desenvolvedores controle total sobre a aparência do programa de instalação. O programa de instalação pode ser gravado para instalar o software adicional, como um aplicativo ODBC. Para obter mais informações sobre os utilitários de instalação do SDK do Windows, consulte a documentação do SDK do Windows.  
  
 A quantidade da instalação é realmente feita pelo programa de instalação depende de quais funções chamadas no instalador do DLL. O DLL do instalador contém funções para instalar os componentes individuais do ODBC. O programa de instalação simplesmente chama **SQLInstallDriverManager**, **SQLInstallDriverEx**, ou **SQLInstallTranslatorEx** no DLL para recuperar o caminho do instalador do diretório no qual o componente está para ser instalado e para adicionar informações sobre o componente no registro. Essas funções, na verdade, não copiar arquivos; o programa de instalação é usar as informações nos argumentos dessas funções.  
  
 O instalador DLL também contém funções para remover os componentes ODBC. O programa de instalação chamar **no SQLRemoveDriverManager**, **no SQLRemoveDriver**, ou **no SQLRemoveTranslator** no instalador do DLL para diminuir o uso de um componente contagem Registro e, se a nova contagem de uso do componente cair para 0, remova todas as informações sobre o componente do registro. Essas funções, na verdade, não remover os arquivos para o componente. o programa de instalação faz isso, se a nova contagem de uso cair para 0.
