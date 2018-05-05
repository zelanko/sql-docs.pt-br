---
title: Conformidade de SQL-92 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d6f256f16960332de497e6a861137ca42a0480f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-92-compliance"></a>Conformidade de SQL-92
Os Drivers de banco de dados de área de trabalho do ODBC e o mecanismo subjacente do Microsoft Jet não são compatíveis com o SQL-92. Eles oferecem suporte a muitos recursos que foram definidos em SQL-92. Não há suporte para alguns recursos com suporte no driver em SQL-92. Para obter mais informações, consulte o *guia do programador do Microsoft Jet Database Engine*. A seguir está as principais diferenças entre os dois:  
  
-   O SQL usado pelos Drivers de banco de dados da área de trabalho suporta expressões mais complexas que o especificado pelo SQL-92.  
  
-   Aplicam regras diferentes para o predicado BETWEEN.  
  
-   O SQL usado pelos Drivers de banco de dados de área de trabalho e ANSI SQL oferece suporte a palavras-chave diferentes.  
  
 Não há suporte para os seguintes recursos do SQL-92 SQL do Microsoft Jet:  
  
-   Instruções de segurança, como GRANT e bloqueio.  
  
-   DISTINCT com referências de função de agregação.  
  
 Os recursos a seguir são aprimoramentos no SQL usada pelos Drivers de banco de dados de área de trabalho que não são especificados pelo SQL-92:  
  
-   A instrução de TRANSFORMAÇÃO fornecendo suporte para consultas de tabela de referência cruzada.  
  
-   Funções de agregação adicionais (**StDev** e **VarP**).  
  
> [!NOTE]  
>  Os Drivers de banco de dados de área de trabalho oferecem suporte a sintaxe ANSI padrão para % (porcentagem) e _ (sublinhado), não * (asterisco) e? (ponto de interrogação).
