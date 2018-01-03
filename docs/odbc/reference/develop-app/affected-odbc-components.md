---
title: Componentes ODBC afetados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e74a2a77a224fd4ef7e48f9211857d42732d84dc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="affected-odbc-components"></a>Componentes ODBC afetados
Compatibilidade com versões anteriores descreve como os aplicativos, o Gerenciador de Driver e os drivers são afetados pela introdução de uma nova versão do Gerenciador de Driver. Isso afeta a aplicativos e o driver quando um ou ambos os parâmetros permanecem na versão antiga. Há, portanto, três tipos de compatibilidade com versões anteriores a serem consideradas, conforme mostrado na tabela a seguir.  
  
|Tipo|Versão do DM|Versão do aplicativo|Versão do driver|  
|----------|-------------------|----------------------------|-----------------------|  
|Compatibilidade com versões anteriores do Gerenciador de Driver|3*. x*|2.*x*|2.*x*|  
|Compatibilidade com versões anteriores do Driver [1]|3*. x*|2.*x*|3.*x*|  
|Compatibilidade com versões anteriores do aplicativo|3.*x*|3.*x*|2.*x*|  
  
 [1] a compatibilidade com versões anteriores dos drivers principalmente é discutida no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
> [!NOTE]  
>  Um aplicativo compatível com os padrões — por exemplo, um aplicativo que tenha sido gravado de acordo com os padrões de Open Group ou ISO CLI — é garantido para trabalhar com um ODBC 3*. x* driver por meio de ODBC 3*. x*Gerenciador de driver. Presume-se que a funcionalidade que o aplicativo está usando está disponível no driver. Presume-se também que o aplicativo compatível com os padrões foi compilado com o ODBC 3*. x* arquivos de cabeçalho.
