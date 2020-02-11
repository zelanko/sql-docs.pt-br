---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4d4b3d8d417591bd72dde22240c81a91d80f990
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948979"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de acesso. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando o driver do Microsoft Access é usado, SQL_COMMIT e SQL_ROLLBACK têm suporte para o argumento *ftype* em uma chamada para **SQLTransact**.  
  
 Se ocorrer uma falha durante o processo de confirmação, o banco de dados afetado poderá ser reparado usando a opção reparar banco de dados na instalação do driver do Microsoft Access ou por meio do uso da palavra-chave REPAIR_DB na função **SQLConfigDataSource** .
