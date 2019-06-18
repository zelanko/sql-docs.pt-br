---
title: Criando e encerrando Threads | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9d6d15c449d88043e844addd12ac10a98d5c4a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470864"
---
# <a name="creating-and-terminating-threads"></a>Criar e encerrar threads
Aplicativos multithread que usam ODBC devem chamar o Microsoft® Visual C++® funções da biblioteca em tempo de execução **beginthread** e **endthread** (ou **beginthreadex**e **endthreadex**) para criar e encerrar threads que chamam o Gerenciador de Driver ODBC. Se os aplicativos chamam as funções Microsoft Windows NT® **CreateThread** e **EndThread** em vez disso, a memória vazamentos ocorrerá porque o Gerenciador de Driver e alguns drivers ODBC chamam de tempo de execução C funções fornecidas pelo não funcionará em um thread criado chamando **CreateThread**. Para obter mais informações, consulte a documentação de Microsoft Windows®.
