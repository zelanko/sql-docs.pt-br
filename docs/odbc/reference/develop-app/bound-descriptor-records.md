---
title: Registros de descritor associados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d0016a2849feb5656cb3cd6dd46eff444f37058
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118758"
---
# <a name="bound-descriptor-records"></a>Registros de descritor associados
Quando o aplicativo define o campo SQL_DESC_DATA_PTR de um registro de descritor para que ele não contém um valor nulo, o registro será considerado *vinculado*.  
  
 Se o descritor for um APD, cada registro acoplado constitui um parâmetro associado. Para parâmetros de entrada, o aplicativo deve associar um parâmetro para cada marcador de parâmetro dinâmico na instrução SQL antes de executar a instrução. Para parâmetros de saída, o aplicativo não precisa associar o parâmetro.  
  
 Se o descritor for descartar um, que descreve uma linha de dados do banco de dados, cada registro acoplado constitui uma coluna associada.
