---
description: SQLTransact (Driver do Access)
title: SQLTransact (driver de acesso) | Microsoft Docs
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
ms.openlocfilehash: 7e9b00f8f5a12af2d3823171d22ad53106569352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339654"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de acesso. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando o driver do Microsoft Access é usado, SQL_COMMIT e SQL_ROLLBACK têm suporte para o argumento *ftype* em uma chamada para **SQLTransact**.  
  
 Se ocorrer uma falha durante o processo de confirmação, o banco de dados afetado poderá ser reparado usando a opção reparar banco de dados na instalação do driver do Microsoft Access ou por meio do uso da palavra-chave REPAIR_DB na função **SQLConfigDataSource** .
