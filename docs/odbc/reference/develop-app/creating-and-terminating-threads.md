---
title: Criando e encerrando Threads | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6568dd1109dc417cad0e5f4ad3d973ae5aaa497a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="creating-and-terminating-threads"></a>Criando e encerrando Threads
Aplicativos multithread que usam ODBC devem chamar as funções de biblioteca de tempo de execução do Microsoft® Visual C++® **beginthread** e **endthread** (ou **beginthreadex** e **endthreadex**) para criar e encerrar segmentos que chamam o Gerenciador de Driver ODBC. Se os aplicativos chamam as funções Microsoft Windows NT® **CreateThread** e **EndThread** em vez disso, memória vazamentos ocorrerá porque o Gerenciador de Driver e alguns drivers ODBC chamada de tempo de execução C funções não funcionará em um thread criado chamando **CreateThread**. Para obter mais informações, consulte a documentação de Microsoft Windows®.
