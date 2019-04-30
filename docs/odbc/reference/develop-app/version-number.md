---
title: Número de versão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- version number supported [ODBC]
- interoperability [ODBC], version number supported
ms.assetid: 6eccacdf-b837-4b66-bd48-ba31771acecb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03678023990fc15d03c73501f331ecc302f6b892
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208441"
---
# <a name="version-number"></a>Número de Versão
Há várias versões do ODBC, cada um com diferentes recursos. Um aplicativo determina qual versão do ODBC o Gerenciador de Driver e um driver específico que dão suporte chamando **SQLGetInfo** com as opções SQL_ODBC_VER e SQL_DRIVER_ODBC_VER.
