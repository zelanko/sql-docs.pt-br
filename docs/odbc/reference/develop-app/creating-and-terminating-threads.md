---
title: Criando e encerrando Threads | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 62950dba2174baac8e3bc34c60f268e07304fa5a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="creating-and-terminating-threads"></a>Criando e encerrando Threads
Aplicativos multithread que usam ODBC devem chamar as funções de biblioteca de tempo de execução do Microsoft® Visual C++® **beginthread** e **endthread** (ou **beginthreadex** e **endthreadex**) para criar e encerrar segmentos que chamam o Gerenciador de Driver ODBC. Se os aplicativos chamam as funções Microsoft Windows NT® **CreateThread** e **EndThread** em vez disso, memória vazamentos ocorrerá porque o Gerenciador de Driver e alguns drivers ODBC chamada de tempo de execução C funções não funcionará em um thread criado chamando **CreateThread**. Para obter mais informações, consulte a documentação de Microsoft Windows®.
