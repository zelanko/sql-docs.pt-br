---
title: Registros de descritor de associado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: acb8d22cc7d2af1efca121c70e99137df88f282b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="bound-descriptor-records"></a>Registros de descritor associados
Quando o aplicativo define o campo SQL_DESC_DATA_PTR de um registro de descritor para que ele não contém um valor nulo, o registro será considerado *associado*.  
  
 Se o descritor é um APD, cada registro associado constitui um parâmetro associado. Para parâmetros de entrada, o aplicativo deve associar um parâmetro para cada marcador de parâmetro dinâmico na instrução SQL antes de executar a instrução. Parâmetros de saída, o aplicativo não precisa associar o parâmetro.  
  
 Se o descritor é um descartar, que descreve uma linha de dados do banco de dados, cada registro associado constitui uma coluna associada.
