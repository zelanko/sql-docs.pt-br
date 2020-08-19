---
description: Componentes ODBC afetados
title: Componentes ODBC afetados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4874a22d441ec856c25e08dc20cf04e0f0be89cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424858"
---
# <a name="affected-odbc-components"></a>Componentes ODBC afetados
A compatibilidade com versões anteriores descreve como os aplicativos, o Gerenciador de driver e os drivers são afetados pela introdução de uma nova versão do Gerenciador de driver. Isso afeta aplicativos e drivers quando um ou ambos permanecem na versão antiga. Há, portanto, três tipos de compatibilidade com versões anteriores a serem consideradas, conforme mostrado na tabela a seguir.  
  
|Type|Versão do DM|Versão do aplicativo|Versão do driver|  
|----------|-------------------|----------------------------|-----------------------|  
|Compatibilidade com versões anteriores do Gerenciador de driver|*3.x*|*2. x*|*2. x*|  
|Compatibilidade com versões anteriores do driver [1]|*3.x*|*2. x*|*3.x*|  
|Compatibilidade com versões anteriores do aplicativo|*3.x*|*3.x*|*2. x*|  
  
 [1] a compatibilidade com versões anteriores dos drivers é discutida principalmente no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
  
> [!NOTE]
>  Um aplicativo compatível com padrões, por exemplo, um aplicativo que foi escrito de acordo com os padrões de grupo aberto ou CLI ISO-tem a garantia de funcionar com um driver ODBC *3. x* por meio do Gerenciador de driver ODBC *3. x* . Supõe-se que a funcionalidade que o aplicativo está usando está disponível no driver. Também pressupõe-se que o aplicativo em conformidade com os padrões tenha sido compilado com os arquivos de cabeçalho ODBC *3. x* .
