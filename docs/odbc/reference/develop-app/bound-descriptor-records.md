---
title: Bound Dscriptor Records | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 155ef4951abddc7a73d9d4abfbc45248f33d653c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306303"
---
# <a name="bound-descriptor-records"></a>Registros de descritor associados
Quando o aplicativo define o campo SQL_DESC_DATA_PTR de um registro descritor para que ele não contenha mais um valor nulo, diz-se que o registro está *vinculado*.  
  
 Se o descritor for uma APD, cada registro vinculado constitui um parâmetro vinculado. Para parâmetros de entrada, o aplicativo deve vincular um parâmetro para cada marcador de parâmetro dinâmico na declaração SQL antes de executar a declaração. Para parâmetros de saída, a aplicação não precisa vincular o parâmetro.  
  
 Se o descritor for um ARD, que descreve uma linha de dados do banco de dados, cada registro vinculado constitui uma coluna vinculada.
