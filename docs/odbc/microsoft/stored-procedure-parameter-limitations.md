---
title: Limitações de parâmetros de procedimento armazenados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd748884575791d5f170e95bc5aa465b61624b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299196"
---
# <a name="stored-procedure-parameter-limitations"></a>Limitações do parâmetro de procedimento armazenado
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Ao executar procedimentos armazenados pela Oracle que utilizam 10 ou mais parâmetros de saída, a chamada de procedimento armazenado falhará, resultando em um erro de Violação de Acesso ou Objetos de Dados ActiveX (ADO). Isso pode ocorrer ao usar o Microsoft ODBC Driver for Oracle com versões 8.0.4.0.0 e 8.0.4.0.4 do software cliente Oracle.  
  
 Para corrigir o problema, o software cliente Oracle deve ser atualizado para a versão 8.0.4.2.0 ou superior. Entre em contato com a Oracle Corporation para obter mais informações sobre os [patches](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!NOTE]  
>  Esse problema não ocorre com a versão inicial do software cliente Oracle versão 8.0.3.0.0.
