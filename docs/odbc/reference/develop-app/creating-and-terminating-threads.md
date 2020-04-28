---
title: Criando e encerrando threads | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3536deef604d7dbf645903e7d171a58cd9fec96a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301687"
---
# <a name="creating-and-terminating-threads"></a>Criar e encerrar threads
Os aplicativos multithread que usam o ODBC devem chamar o Microsoft® Visual C++® funções de biblioteca de tempo de execução **_beginthread** e **_endthread** (ou **_beginthreadex** e **_endthreadex**) para criar e encerrar threads que chamam o Gerenciador de driver ODBC. Se os aplicativos chamarem o Microsoft Windows NT® Functions **CreateThread** e **endthread** em vez disso, ocorrerão vazamentos de memória porque o Gerenciador de driver e alguns drivers ODBC chamam as funções de tempo de execução C que não funcionarão em um thread criado chamando **CreateThread**. Para obter mais informações, consulte a documentação do Microsoft Windows®.
