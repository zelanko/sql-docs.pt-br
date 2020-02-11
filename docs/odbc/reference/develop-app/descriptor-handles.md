---
title: Identificadores de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 24e3d4c87f3bc461a339a6cb635d64f20dc73e20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106159"
---
# <a name="descriptor-handles"></a>Identificadores de descritor
Um *descritor* é uma coleção de metadados que descreve os parâmetros de uma instrução SQL ou as colunas de um conjunto de resultados, como visto pelo aplicativo ou driver (também conhecido como *implementação*). Assim, um descritor pode preencher qualquer uma das quatro funções:  
  
-   **Descritor de parâmetro de aplicativo (APD).** Contém informações sobre os buffers de aplicativo associados aos parâmetros em uma instrução SQL, como seus endereços, comprimentos e tipos de dados C.  
  
-   **Descritor de parâmetro de implementação (IPD).** Contém informações sobre os parâmetros em uma instrução SQL, como seus tipos de dados SQL, comprimentos e nulidade.  
  
-   **Descritor de linha do aplicativo (ARD).** Contém informações sobre os buffers de aplicativo associados às colunas em um conjunto de resultados, como seus endereços, comprimentos e tipos de dados de C.  
  
-   **Descritor de linha de implementação (IRD).** Contém informações sobre as colunas em um conjunto de resultados, como seus tipos de dados SQL, comprimentos e nulidade.  
  
 Quatro descritores (um preenchimento de cada função) são alocados automaticamente quando uma instrução é alocada. Eles são conhecidos como *descritores alocados automaticamente* e sempre são associados a essa instrução. Os aplicativos também podem alocar descritores com **SQLAllocHandle**. Eles são conhecidos como *descritores explicitamente alocados*. Eles são alocados em uma conexão e podem ser associados a uma ou mais instruções nessa conexão para atender à função de um APD ou ARD nessas instruções.  
  
 A maioria das operações no ODBC pode ser executada sem o uso explícito de descritores pelo aplicativo. No entanto, os descritores fornecem um atalho conveniente para algumas operações. Por exemplo, suponha que um aplicativo queira inserir dados de dois conjuntos diferentes de buffers. Para usar o primeiro conjunto de buffers, ele chamaria repetidamente **SQLBindParameter** para associá-los aos parâmetros em uma instrução **Insert** e, em seguida, executar a instrução. Para usar o segundo conjunto de buffers, ele repetiria esse processo. Como alternativa, ele poderia configurar associações para o primeiro conjunto de buffers em um descritor e para o segundo conjunto de buffers em outro descritor. Para alternar entre os conjuntos de associações, o aplicativo simplesmente chamaria **SQLSetStmtAttr** e associaria o descritor correto à instrução como APD.  
  
 Para obter mais informações sobre descritores, consulte [tipos de descritores](../../../odbc/reference/develop-app/types-of-descriptors.md).
