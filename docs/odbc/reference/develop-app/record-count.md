---
title: Contagem de registros | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281812"
---
# <a name="record-count"></a>Contagem de registros
O campo de cabeçalho de SQL_DESC_COUNT de um descritor é o índice baseado em um do registro de numeração mais alto que contém dados. Esse campo não é uma contagem de todas as colunas ou parâmetros associados. Quando um descritor é alocado, o valor inicial de SQL_DESC_COUNT é 0.  
  
 O driver executa qualquer ação necessária para alocar e manter qualquer armazenamento necessário para manter as informações do descritor. O aplicativo não especifica explicitamente o tamanho de um descritor nem aloca novos registros. Quando o aplicativo fornece informações para um registro de descritor cujo número é maior que o valor de SQL_DESC_COUNT, o driver aumenta automaticamente SQL_DESC_COUNT. Quando o aplicativo desassocia o registro de descritor de numeração mais alto, o driver diminui automaticamente SQL_DESC_COUNT para conter o número do registro associado restante mais alto.
