---
title: SQLTransact (Motorista de Acesso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f88d3154925ab589a8519cb9205da03e8c3dc08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299256"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do Access Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando o driver do Microsoft Access é usado, SQL_COMMIT e SQL_ROLLBACK são suportados para o argumento *fType* em uma chamada para **SQLTransact**.  
  
 Se ocorrer uma falha durante o processo de confirmação, o banco de dados afetado pode ser reparado usando a opção 'Reparar banco de dados' na configuração do driver Microsoft Access ou através do uso da palavra-chave REPAIR_DB na função **SQLConfigDataSource.**
