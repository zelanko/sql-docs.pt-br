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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4d684fb6d9614defdca3897c53c4bae9fc231a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138079"
---
# <a name="record-count"></a>Contagem de registros
O campo de cabeçalho de SQL_DESC_COUNT de um descritor é o índice baseado em um do registro de numeração mais alto que contém dados. Esse campo não é uma contagem de todas as colunas ou parâmetros associados. Quando um descritor é alocado, o valor inicial de SQL_DESC_COUNT é 0.  
  
 O driver executa qualquer ação necessária para alocar e manter qualquer armazenamento necessário para manter as informações do descritor. O aplicativo não especifica explicitamente o tamanho de um descritor nem aloca novos registros. Quando o aplicativo fornece informações para um registro de descritor cujo número é maior que o valor de SQL_DESC_COUNT, o driver aumenta automaticamente SQL_DESC_COUNT. Quando o aplicativo desassocia o registro de descritor de numeração mais alto, o driver diminui automaticamente SQL_DESC_COUNT para conter o número do registro associado restante mais alto.
