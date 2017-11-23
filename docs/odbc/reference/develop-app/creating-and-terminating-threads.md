---
title: Criando e encerrando Threads | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a30fbe976ac3de550f8067cca82732631f698ac
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="creating-and-terminating-threads"></a>Criando e encerrando Threads
Aplicativos multithread que usam ODBC devem chamar as funções de biblioteca de tempo de execução do Microsoft® Visual C++® **beginthread** e **endthread** (ou **beginthreadex** e **endthreadex**) para criar e encerrar segmentos que chamam o Gerenciador de Driver ODBC. Se os aplicativos chamam as funções Microsoft Windows NT® **CreateThread** e **EndThread** em vez disso, memória vazamentos ocorrerá porque o Gerenciador de Driver e alguns drivers ODBC chamada de tempo de execução C funções não funcionará em um thread criado chamando **CreateThread**. Para obter mais informações, consulte a documentação de Microsoft Windows®.

