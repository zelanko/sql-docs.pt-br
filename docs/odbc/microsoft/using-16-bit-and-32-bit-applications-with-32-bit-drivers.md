---
title: Uso de aplicativos de 16 bits e 32 bits com Drivers de 32 bits | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 802b09dd83ce3671edbff33ff2be447c6279621f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>Uso de aplicativos de 16 bits e 32 bits com Drivers de 32 bits
> [!IMPORTANT]  
>  suporte a aplicativos de 16 bits será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Desenvolva aplicativos de 32 bits ou 64 bits em vez disso.  
  
 Com o componente de acesso de dados ODBC, você pode usar aplicativos de 16 bits e 32 bits com drivers de 32 bits. As seguintes combinações de aplicativos e drivers de suporte a sistemas operacionais Microsoft® Windows® 95/98 e Microsoft Windows/Windows 2000:  
  
-   aplicativos de 16 bits com drivers de 32 bits  
  
-   aplicativos de 32 bits com drivers de 32 bits  
  
 Não há suporte para usar um aplicativo de 32 bits com um driver de 16 bits.  
  
> [!NOTE]  
>  Começando com a versão do ODBC versão 3.0, Windows NT 4.0 são suportados.  
  
 ODBC inclui os componentes ODBC necessários para oferecer suporte as configurações acima por "conversão" bibliotecas de vínculo dinâmico (DLLs) para converter os endereços de 16 bits para endereços de 32 bits e vice-versa. O programa de instalação determina qual sistema operacional você está usando e instala os componentes ODBC exigidos pelo sistema. Você também pode optar por instalar os componentes ODBC usados por todos os sistemas.  
  
 Na maioria dos casos, portando um aplicativo ou driver de 16 bits para 32 bits envolve cinco tipos de alterações:  
  
-   Alterações no código de tratamento de mensagens  
  
-   Alterações porque inteiros e identificadores de 32 bits  
  
-   Alterações em chamadas para interfaces de programação de aplicativo (APIs) do Windows  
  
-   Alterações para tornar o driver thread-safe  
  
-   Alterações nos componentes ODBC  
  
 Do ponto de vista programação do aplicativo ou driver, a principal diferença entre os componentes ODBC de 16 bits e 32 bits é que eles tenham nomes de arquivo diferente. Do ponto de vista de sistema, a arquitetura de cada conexão de aplicativo ou driver é diferente e as ferramentas usadas para gerenciar fontes de dados são diferentes.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Usando aplicativos de 16 bits com drivers de 32 bits](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [Usando aplicativos de 32 bits com drivers de 32 bits](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
