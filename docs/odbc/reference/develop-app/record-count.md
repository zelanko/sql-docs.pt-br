---
title: Contagem de registros | Microsoft Docs
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
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca1ed60d44b1c8133c51e78a769ca6d92d9bb6b0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="record-count"></a>Contagem de registros
O campo de cabeçalho SQL_DESC_COUNT de um descritor de é o índice baseado em um do registro de número mais alto que contém dados. Este campo não é uma contagem de todas as colunas ou parâmetros que estão associados. Quando um descritor é alocado, o valor inicial de SQL_DESC_COUNT é 0.  
  
 O driver executa qualquer ação necessário para alocar e manter qualquer armazenamento requer para manter informações de descritor. O aplicativo não foi explicitamente especificar o tamanho de um descritor nem alocar novos registros. Quando o aplicativo fornece informações para um registro de descritor cujo número for maior que o valor de SQL_DESC_COUNT, o driver automaticamente aumenta SQL_DESC_COUNT. Quando o aplicativo desassocia o registro do descritor de número mais alto, o driver automaticamente diminui SQL_DESC_COUNT para conter o número do registro associado restante mais alto.
