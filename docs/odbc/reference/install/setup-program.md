---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f64eda5ad640e50afd25db111de74141e41e652d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280775"
---
# <a name="setup-program"></a>Programa de instalação
> **OBSERVAÇÃO:** Começando com o Windows XP e Windows Server 2003, **ODBC está incluído no sistema operacional Windows**. Você deve instalar apenas explicitamente ODBC em versões anteriores do Windows.  
  
 O usuário executa o programa de instalação para iniciar o processo de instalação. O programa de instalação é escrito pelo desenvolvedor do aplicativo ou driver. Além de instalar os componentes de ODBC, ele poderá instalar outros softwares. Por exemplo, os desenvolvedores de aplicativos podem usar o mesmo programa de instalação para instalar os componentes ODBC e instalar seus aplicativos.  
  
 Os desenvolvedores podem escrever o programa de instalação do zero, usando os utilitários de configuração do SDK do Microsoft® Windows® ou instalar o software de outros fornecedores. Isso fornece aos desenvolvedores controle completo sobre a aparência do programa de configuração. O programa de instalação pode ser gravado para instalar software adicional, como um aplicativo ODBC. Para obter mais informações sobre os utilitários de instalação do SDK do Windows, consulte a documentação do SDK do Windows.  
  
 Quanto da instalação é realmente realizado pelo programa de instalação depende de quais funções chamadas no instalador do DLL. A DLL do instalador contém funções para instalar os componentes individuais do ODBC. O programa de instalação simplesmente chama **SQLInstallDriverManager**, **SQLInstallDriverEx**, ou **SQLInstallTranslatorEx** no instalador do DLL para recuperar o caminho das diretório no qual o componente está para ser instalado e para adicionar informações sobre o componente no registro. Essas funções, na verdade, não copie arquivos; o programa de instalação faz isso usando as informações nos argumentos de uma dessas funções.  
  
 O instalador do DLL também contém funções para remover componentes ODBC. As chamadas do programa de instalação **SQLRemoveDriverManager**, **SQLRemoveDriver**, ou **SQLRemoveTranslator** no instalador do DLL para diminuir o uso de um componente contar no Registro e, se a nova contagem de uso do componente cai a 0, remova todas as informações sobre o componente do registro. Essas funções, na verdade, não remover os arquivos para o componente; o programa de instalação faz isso, se a nova contagem de uso cair para 0.
