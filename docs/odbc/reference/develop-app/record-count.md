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
manager: craigg
ms.openlocfilehash: 8f8b0a6fc7aa5765d9373af33ab4fac0a4a07aac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151232"
---
# <a name="record-count"></a>Contagem de registros
O campo de cabeçalho de um descritor de SQL_DESC_COUNT é o índice baseado em um do registro de número mais alto que contém dados. Este campo não é uma contagem de todas as colunas ou parâmetros que estão associados. Quando um descritor é alocado, o valor inicial de SQL_DESC_COUNT é 0.  
  
 O driver usa qualquer ação necessárias para alocar e manter qualquer armazenamento que ele necessita para manter informações de descritor. O aplicativo não foi explicitamente especificar o tamanho de um descritor nem alocar novos registros. Quando o aplicativo fornece informações para um registro de descritor cujo número é maior do que o valor de SQL_DESC_COUNT, o driver aumenta automaticamente SQL_DESC_COUNT. Quando o aplicativo desassocia o registro do descritor de número mais alto, o driver diminui automaticamente SQL_DESC_COUNT para conter o número do maior registro associado restante.
