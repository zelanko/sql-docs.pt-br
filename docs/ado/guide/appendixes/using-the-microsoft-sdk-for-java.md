---
title: Usando o SDK do Microsoft para Java | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76fb8068cfc1640642292932923db084818dbb9c
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270015"
---
# <a name="using-the-microsoft-sdk-for-java"></a>Usando o SDK do Microsoft para Java

> [!IMPORTANT]
> Microsoft foi descontinuado suporte do Visual J++ em janeiro de 2004.

O SDK do Microsoft para Java é o kit de desenvolvedor para o ambiente do Microsoft Internet Explorer. Ferramentas, informações e exemplos são fornecidos para ajudar você a desenvolver programas de Java e miniaplicativos com base em JDK 1.1 e a máquina virtual do Microsoft Win32 (Microsoft VM). O SDK do Microsoft para Java não está vinculado ao Microsoft Visual J++. Para baixar o SDK, clique aqui.  
  
 O utilitário Jactivex.exe gera classes de uma biblioteca de tipos, mas só pode ser chamado na linha de comando. Este recurso não está integrado com o ambiente de desenvolvimento Visual J++. Ao contrário das classes geradas pelo Assistente de biblioteca de tipo de Java, você pode percorrer os wrappers de classe criados pelo SDK. Isso é útil para depuração como seu código usa as classes de wrapper do ADO.  
  
 Esse mecanismo lê a biblioteca de tipos do ADO e gera classes que você pode instanciar dentro de seu aplicativo. Ele gera essas classes no seguinte local: \\< diretório do windows\>\Java\trustlib\msado15.  
  
 Criar um aplicativo ADO em Java usando o SDK do Microsoft para Java é basicamente idêntico, da perspectiva do código-fonte, usando o Assistente de biblioteca de tipo de Java. Para exemplo de código, consulte [ADO Java classe Wrappers](../../../ado/guide/appendixes/ado-java-class-wrappers.md). É a única diferença na forma de gerar as classes de wrapper em primeiro lugar, conforme mostrado nas etapas a seguir.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Para criar um projeto de ADO com o Microsoft SDK para Java  
  
1.  Execute o seguinte no prompt de comando. Você deve definir o caminho para incluir o SDK do Microsoft para o diretório Bin do Java, ou execute o comando nesse local. Normalmente, o SDK do Microsoft para Java é instalado no mesmo local que o Visual Studio. Esta é uma instrução de único comando.  
  
    ```  
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  Execute o seguinte comando para compilar as classes geradas. A opção /g:t ativa a geração de símbolos de depuração para que você pode rastrear para o. Símbolos de Java. Remova-o para compilações de versão.  
  
    ```  
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  Para usar esses arquivos, abra seu projeto no Visual J++. Do **projeto** menu, escolha **adicionar ao projeto**. Selecione **arquivos**e adicionar todos os. Arquivos de JAVA gerados no diretório trustlib\msado15 ao seu projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Wrappers de classe Java ADO](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
