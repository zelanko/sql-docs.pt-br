---
title: Contagem de discos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28e503ae4602d87fc9138ed018ee1e95f135ec57
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281812"
---
# <a name="record-count"></a>Contagem de registros
O campo de cabeçalho SQL_DESC_COUNT de um descritor é o índice único do registro de maior numeração que contém dados. Este campo não é uma contagem de todas as colunas ou parâmetros que estão vinculados. Quando um descritor é alocado, o valor inicial de SQL_DESC_COUNT é 0.  
  
 O motorista toma todas as medidas necessárias para alocar e manter qualquer armazenamento necessário para armazenar informações do descritor. O aplicativo não especifica explicitamente o tamanho de um descritor nem aloca novos registros. Quando o aplicativo fornece informações para um registro de descritor cujo número é maior do que o valor de SQL_DESC_COUNT, o motorista aumenta automaticamente SQL_DESC_COUNT. Quando o aplicativo desvincula o registro de descritor com maior numeração, o driver diminui automaticamente SQL_DESC_COUNT para conter o número do registro de limite mais alto restante.
