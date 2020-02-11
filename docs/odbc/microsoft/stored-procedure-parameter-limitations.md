---
title: Limitações de parâmetro de procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f1c5a18eb9f0b1939a2c3602f1ebe7695741f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948824"
---
# <a name="stored-procedure-parameter-limitations"></a>Limitações do parâmetro de procedimento armazenado
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Ao executar procedimentos armazenados Oracle que utilizam 10 ou mais parâmetros de saída, a chamada de procedimento armazenado falhará, resultando em uma violação de acesso ou um erro de ActiveX Data Objects (ADO). Isso pode ocorrer ao usar o Microsoft ODBC driver for Oracle com versões 8.0.4.0.0 e 8.0.4.0.4 do software cliente Oracle.  
  
 Para corrigir o problema, o software cliente Oracle deve ser atualizado para a versão 8.0.4.2.0 ou superior. Entre em contato com a Oracle Corporation para obter mais informações sobre os [patches](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!NOTE]  
>  Esse problema não ocorre com o lançamento inicial do software cliente Oracle versão 8.0.3.0.0.
