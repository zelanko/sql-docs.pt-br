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
ms.openlocfilehash: b97f29ad06c4ed961f3cee571b0ca7b8d9c0b774
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002086"
---
# <a name="creating-and-terminating-threads"></a>Criar e encerrar threads
Aplicativos multithread que usam ODBC devem chamar o Microsoft® Visual C++® funções da biblioteca em tempo de execução **beginthread** e **endthread** (ou **beginthreadex**e **endthreadex**) para criar e encerrar threads que chamam o Gerenciador de Driver ODBC. Se os aplicativos chamam as funções Microsoft Windows NT® **CreateThread** e **EndThread** em vez disso, a memória vazamentos ocorrerá porque o Gerenciador de Driver e alguns drivers ODBC chamam de tempo de execução C funções fornecidas pelo não funcionará em um thread criado chamando **CreateThread**. Para obter mais informações, consulte a documentação de Microsoft Windows®.
