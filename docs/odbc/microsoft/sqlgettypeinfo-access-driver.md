---
title: SQLGetTypeInfo (driver de acesso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLGetTypeInfo
- SQLGetTypeInfo function [ODBC], Access Driver
ms.assetid: a28b16eb-ca36-4297-9297-ecd7c107a84e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 788f0b8c69636ad9bf93de73632abc911a0fb0e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898760"
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de acesso. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida por **SQLGetTypeInfo** será o nome mais comumente usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE será retornado na coluna PESQUISÁvel para os tipos de dados byte, contador, duplo, único, longo e curto. (O recurso LIKE pode ser obtido convertendo o valor em um caractere usando as funções de conversão canônica ODBC e, em seguida, executando a comparação.)
