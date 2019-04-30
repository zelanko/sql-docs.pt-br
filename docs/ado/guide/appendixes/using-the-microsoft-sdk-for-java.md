---
title: Usando o Microsoft SDK para Java | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab4aaed1cfd661d38476c81f8bdc3dcab3aa0f88
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199740"
---
# <a name="using-the-microsoft-sdk-for-java"></a>Usar o Microsoft SDK para Java

> [!IMPORTANT]
> Microsoft Descontinuado suporte do Visual J++ de janeiro de 2004.

O Microsoft SDK para Java é o kit de desenvolvedor para o ambiente do Microsoft Internet Explorer. Ferramentas, informações e exemplos são fornecidos para ajudar você a desenvolver programas Java e miniaplicativos com base no JDK 1.1 e a máquina virtual do Microsoft Win32 (Microsoft VM). O Microsoft SDK para Java não está vinculado ao Microsoft Visual J++. Para baixar esse SDK, clique aqui.  
  
 O utilitário Jactivex.exe gera classes de uma biblioteca de tipos, mas só pode ser invocado na linha de comando. Esse recurso não está integrado com o ambiente de desenvolvimento Visual J++. Ao contrário das classes geradas pelo Assistente de biblioteca de tipo Java, você poderá intervir os wrappers de classe criados pelo SDK. Isso é útil para depuração como seu código usa as classes de wrapper do ADO.  
  
 Esse mecanismo lê a biblioteca de tipos do ADO e gera classes que você pode criar uma instância dentro de seu aplicativo. Ele gera essas classes no seguinte local: \\< diretório do windows\>\Java\trustlib\msado15.  
  
 Criar um aplicativo ADO em Java usando o Microsoft SDK para Java é basicamente idêntico, da perspectiva do código-fonte, usando o Assistente de biblioteca de tipo Java. Para exemplo de código, consulte [Wrappers de classe Java ADO](../../../ado/guide/appendixes/ado-java-class-wrappers.md). A única diferença está em como você gerar as classes de wrapper em primeiro lugar, conforme demonstrado nas etapas a seguir.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Para criar um projeto do ADO com o Microsoft SDK para Java  
  
1.  Execute o seguinte no prompt de comando. Você deve definir o caminho para incluir o SDK da Microsoft para o diretório Bin do Java ou execute o comando nesse local. Normalmente, o Microsoft SDK para Java é instalado no mesmo local que o Visual Studio. Essa é uma instrução de único comando.  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  Execute o seguinte comando para compilar as classes geradas. O comutador /g:t ativa a geração de símbolos de depuração para que você pode rastrear o. Símbolos de Java. Para removê-lo para compilações de versão.  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  Para usar esses arquivos, abra o projeto no Visual J++. Dos **Project** menu, escolha **adicionar ao projeto**. Selecione **arquivos**e adicionar todos os. Arquivos do JAVA gerados no diretório trustlib\msado15 ao seu projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Wrappers de classe Java ADO](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
