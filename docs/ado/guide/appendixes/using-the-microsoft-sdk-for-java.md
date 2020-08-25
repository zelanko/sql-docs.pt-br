---
description: Usar o Microsoft SDK para Java
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 302cca77222454ac6fa73c69683c641e841acdda
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806487"
---
# <a name="using-the-microsoft-sdk-for-java"></a>Usar o Microsoft SDK para Java

> [!IMPORTANT]
> O Microsoft descontinuau o suporte do Visual J++ em janeiro de 2004.

O Microsoft SDK para Java é o kit para desenvolvedores do ambiente do Microsoft Internet Explorer. Ferramentas, informações e exemplos são fornecidos para ajudá-lo a desenvolver programas e applets Java com base no JDK 1,1 e na máquina virtual Microsoft Win32 (Microsoft VM). O Microsoft SDK para Java não está vinculado ao Microsoft Visual J++. Para baixar esse SDK, clique aqui.  
  
 O utilitário Jactivex.exe gera classes de uma biblioteca de tipos, mas só pode ser invocada na linha de comando. Esse recurso não está integrado ao ambiente de desenvolvimento do Visual J++. Ao contrário das classes geradas pelo assistente de biblioteca de tipos Java, você pode entrar nos wrappers de classe criados pelo SDK. Isso é útil para depurar como seu código usa as classes de wrapper do ADO.  
  
 Esse mecanismo lê a biblioteca de tipos do ADO e gera classes que você pode instanciar dentro de seu aplicativo. Ele gera essas classes no seguinte local: \\<diretório do Windows \> \Java\trustlib\msado15.  
  
 A criação de um aplicativo ADO em Java usando o SDK da Microsoft para Java é fundamentalmente idêntica, da perspectiva do código-fonte, ao uso do assistente da biblioteca de tipos Java. Para obter o código de exemplo, consulte [wrappers de classe Java do ADO](./ado-java-class-wrappers.md). A única diferença real é como você gera as classes de wrapper em primeiro lugar, conforme demonstrado nas etapas a seguir.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Para criar um projeto do ADO com o Microsoft SDK para Java  
  
1.  Execute o seguinte em um prompt de comando. Você deve definir o caminho para incluir o diretório do Microsoft SDK para Java bin ou executar o comando desse local. Normalmente, o Microsoft SDK para Java é instalado no mesmo local que o Visual Studio. Essa é uma única instrução de comando.  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  Execute o comando a seguir para compilar as classes geradas. A opção/g: t ativa a geração de símbolos de depuração para que você possa rastrear no. Símbolos Java. Remova-o para Builds de versão.  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  Para usar esses arquivos, abra o projeto no Visual J++. No menu **projeto** , escolha **Adicionar ao projeto**. Selecione **arquivos**e adicione todos os. Arquivos JAVA gerados no diretório trustlib\msado15 para seu projeto.  
  
## <a name="see-also"></a>Consulte Também  
 [Wrappers de classe Java ADO](./ado-java-class-wrappers.md)