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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b97f29ad06c4ed961f3cee571b0ca7b8d9c0b774
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002086"
---
# <a name="creating-and-terminating-threads"></a>Criar e encerrar threads
Os aplicativos multithread que usam o ODBC devem chamar o Microsoft® Visual C++® funções de biblioteca de tempo de execução **_beginthread** e **_endthread** (ou **_beginthreadex** e **_endthreadex**) para criar e encerrar threads que chamam o Gerenciador de driver ODBC. Se os aplicativos chamarem o Microsoft Windows NT® Functions **CreateThread** e **endthread** em vez disso, ocorrerão vazamentos de memória porque o Gerenciador de driver e alguns drivers ODBC chamam as funções de tempo de execução C que não funcionarão em um thread criado chamando **CreateThread**. Para obter mais informações, consulte a documentação do Microsoft Windows®.
