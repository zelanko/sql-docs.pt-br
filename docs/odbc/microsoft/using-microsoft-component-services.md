---
title: Usando serviços de componentes da Microsoft | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 71c78c6879645fd4f323ca79a7f77911350810c6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632908"
---
# <a name="using-microsoft-component-services"></a>Usar os serviços de componentes da Microsoft
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode habilitar um banco de dados Oracle trabalhar com serviços de componentes transacionais (ou MTS, se você estiver usando o Windows NT) no Microsoft Windows NT/Windows 2000 e no Microsoft Windows 95/98. Para habilitar um banco de dados Oracle trabalhar com os serviços de componentes que dão suporte a transações, os administradores do sistema devem criar uma exibição nomeada V$ XATRANS$. Para criar esse script, você deve executar um script fornecido pelo Oracle. Para obter mais informações, consulte a Ajuda de serviços de componente ou a documentação do Oracle.
