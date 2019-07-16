---
title: SQLTransact (Driver do Access) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948979"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Access. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando o driver do Microsoft Access for usado, SQL_COMMIT e SQL_ROLLBACK têm suporte para o *fType* argumento em uma chamada para **SQLTransact**.  
  
 Se ocorrer uma falha durante o processo de confirmação, o banco de dados afetado pode ser reparado usando a opção de banco de dados de reparo na instalação de driver do Microsoft Access ou por meio do uso a palavra-chave REPAIR_DB na **SQLConfigDataSource** função.
