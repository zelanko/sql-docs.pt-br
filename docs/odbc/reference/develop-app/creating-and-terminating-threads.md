---
title: Criação e Terminação de Threads | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301687"
---
# <a name="creating-and-terminating-threads"></a>Criar e encerrar threads
Os aplicativos multithread que usam o ODBC devem ligar para as funções da Biblioteca de Tempo de Execução microsoft® Visual C+® **_beginthread** e **_endthread** (ou **_beginthreadex** e **_endthreadex)** para criar e encerrar threads que chamam de Gerenciador de Driver ODBC. Se os aplicativos chamarem as funções do Microsoft Windows NT® **CreateThread** e **EndThread,** em vez disso, os vazamentos de memória ocorrerão porque o Driver Manager e alguns drivers ODBC chamam funções de tempo de execução C que não funcionarão em um segmento criado pela chamada **CreateThread**. Para obter mais informações, consulte a documentação ® Microsoft Windows.
