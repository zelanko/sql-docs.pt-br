---
title: Usando os serviços de componentes da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91d6dcf0ca7f87d6ed510d582f7a7ba0f80e8c74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088155"
---
# <a name="using-microsoft-component-services"></a>Usar os serviços de componentes da Microsoft
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode habilitar um banco de dados Oracle para trabalhar com serviços de componentes transacionais (ou MTS, se você estiver usando o Windows NT) no Microsoft Windows NT/Windows 2000 e no Microsoft Windows 95/98. Para permitir que um banco de dados Oracle funcione com serviços de componentes que dão suporte a transações, os administradores de sistema devem criar uma exibição chamada V $ XATRANS $. Para criar esse script, você deve executar um script fornecido pela Oracle. Para obter mais informações, consulte a ajuda dos serviços de componentes ou a documentação do Oracle.
