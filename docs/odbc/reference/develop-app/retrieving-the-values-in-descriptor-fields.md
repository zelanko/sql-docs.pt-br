---
title: Recuperando os valores em campos de descritores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43467d19f3f2e576efa0402c4ba513e23da59390
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304317"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recuperar os valores nos campos de descritor
Um aplicativo pode chamar **SQLGetDescField** para obter um único campo de um registro descritor. **O SQLGetDescField** dá ao aplicativo acesso a todos os campos de descritor definidos no ODBC e também aos campos definidos pelo driver.  
  
 **O SQLGetDescRec** pode ser chamado para recuperar as configurações de vários campos descritores que afetam o tipo de dados e o armazenamento de dados de coluna ou parâmetro.
