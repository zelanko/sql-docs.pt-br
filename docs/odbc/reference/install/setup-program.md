---
title: Programa de Configuração | Microsoft Docs
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
ms.openlocfilehash: b89cae70db65bd2aa54b8e9789a5c2b35696923e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296146"
---
# <a name="setup-program"></a>Programa de instalação
> **NOTA:** Começando com o Windows XP e o Windows Server 2003, **o ODBC está incluído no sistema operacional Windows**. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 O usuário executa o programa de configuração para iniciar o processo de configuração. O programa de configuração é escrito pelo desenvolvedor de aplicativos ou driver. Além de instalar componentes ODBC, ele pode instalar outros softwares. Por exemplo, os desenvolvedores de aplicativos podem usar o mesmo programa de configuração tanto para instalar componentes ODBC quanto para instalar seus aplicativos.  
  
 Os desenvolvedores podem escrever o programa de configuração do zero, usando os utilitários de configuração SDK do Microsoft® Windows® ou software de configuração de outros fornecedores. Isso dá a esses desenvolvedores controle completo sobre a aparência do programa de configuração. O programa de configuração pode ser gravado para instalar software adicional, como um aplicativo ODBC. Para obter mais informações sobre os utilitários de configuração do Windows SDK, consulte a documentação do Windows SDK.  
  
 Quanto da instalação é realmente feita pelo programa de configuração depende de quais funções ele chama no instalador DLL. O instalador DLL contém funções para instalar componentes ODBC individuais. O programa de configuração simplesmente chama **SQLInstallDriverManager,** **SQLInstallDriverEx**ou **SQLInstallTranslatorEx** no instalador DLL para recuperar o caminho do diretório no qual o componente deve ser instalado e adicionar informações sobre o componente ao registro. Essas funções não copiam arquivos; o programa de configuração faz isso usando as informações nos argumentos dessas funções.  
  
 O instalador DLL também contém funções para remover componentes ODBC. O programa de configuração chama **SQLRemoveDriverManager,** **SQLRemoveDriver**ou **SQLRemoveTranslator** no instalador DLL para diminuir a contagem de uso de um componente no registro e, se a nova contagem de uso do componente cair para 0, remova todas as informações sobre o componente do registro. Essas funções não removem os arquivos do componente; o programa de configuração faz isso se a nova contagem de uso cair para 0.
