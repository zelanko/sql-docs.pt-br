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
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722374"
---
# <a name="creating-and-terminating-threads"></a>Criar e encerrar threads
Aplicativos multithread que usam ODBC devem chamar as funções de biblioteca de tempo de execução do Microsoft® Visual C++® **beginthread** e **endthread** (ou **beginthreadex** e **endthreadex**) para criar e encerrar threads que chamam o Gerenciador de Driver ODBC. Se os aplicativos chamam as funções Microsoft Windows NT® **CreateThread** e **EndThread** em vez disso, a memória vazamentos ocorrerá porque o Gerenciador de Driver e alguns drivers ODBC chamam de tempo de execução C funções fornecidas pelo não funcionará em um thread criado chamando **CreateThread**. Para obter mais informações, consulte a documentação de Microsoft Windows®.
