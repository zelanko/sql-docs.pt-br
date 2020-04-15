---
title: Usando aplicativos de 16 bits e 32 bits com drivers de 32 bits | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ce996a7c4816d4d14491e226f891904b6cf8c02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307607"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>Using 16-Bit and 32-Bit Applications with 32-Bit Drivers
> [!IMPORTANT]  
>  O suporte a aplicativos de 16 bits será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Desenvolver aplicativos de 32 ou 64 bits em vez disso.  
  
 Com o componente de acesso a dados ODBC, você pode usar aplicativos de 16 bits e 32 bits com drivers de 32 bits. Os sistemas operacionais Microsoft® Windows® 95/98 e Microsoft Windows NT®/Windows 2000 suportam as seguintes combinações de aplicativos e drivers:  
  
-   Aplicativos de 16 bits com drivers de 32 bits  
  
-   Aplicativos de 32 bits com drivers de 32 bits  
  
 O uso de um aplicativo de 32 bits com um driver de 16 bits não é suportado.  
  
> [!NOTE]  
>  Começando com o lançamento da versão 3.0 do ODBC, o Windows NT 4.0 foi suportado.  
  
 O ODBC inclui os componentes ODBC necessários para suportar as configurações acima, "thunking" dynamic-link libraryes (DLLs) para converter endereços de 16 bits em endereços de 32 bits e vice-versa. O programa Configuração determina qual sistema operacional você está usando e instala os componentes ODBC exigidos por esse sistema. Você também pode optar por instalar os componentes ODBC usados por todos os sistemas.  
  
 Na maioria dos casos, a portação de um aplicativo ou driver de 16 bits para 32 bits envolve cinco tipos de alterações:  
  
-   Alterações no código de tratamento de mensagens  
  
-   Mudanças porque inteiros e alças são de 32 bits  
  
-   Alterações nas chamadas para interfaces de programação de aplicativos do Windows (APIs)  
  
-   Alterações para tornar o driver seguro para threads  
  
-   Alterações nos componentes oDBC  
  
 Do ponto de vista da programação de aplicativos ou drivers, a grande diferença entre componentes ODBC de 16 bits e 32 bits é que eles têm nomes de arquivos diferentes. Do ponto de vista do sistema, a arquitetura de cada conexão de aplicativo ou driver é diferente e as ferramentas usadas para gerenciar fontes de dados são diferentes.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Usando aplicativos de 16 bits com drivers de 32 bits](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [Usando aplicativos de 32 bits com drivers de 32 bits](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
