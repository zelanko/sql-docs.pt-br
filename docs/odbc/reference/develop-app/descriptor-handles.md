---
title: Alças do Descritor | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed0595c97f3f4ad92d976c89327a01e25cb5b753
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305907"
---
# <a name="descriptor-handles"></a>Identificadores de descritor
Um *descritor* é uma coleção de metadados que descreve os parâmetros de uma declaração SQL ou as colunas de um conjunto de resultados, como visto pelo aplicativo ou driver (também conhecido como *implementação*). Assim, um descritor pode preencher qualquer uma das quatro funções:  
  
-   **Descritor de parâmetros de aplicação (APD).** Contém informações sobre os buffers de aplicativo vinculados aos parâmetros em uma declaração SQL, como seus endereços, comprimentos e tipos de dados C.  
  
-   **Descritor de parâmetros de implementação (IPD).** Contém informações sobre os parâmetros em uma declaração SQL, como seus tipos de dados SQL, comprimentos e nulidade.  
  
-   **Descritor de linha de aplicativo (ARD).** Contém informações sobre os buffers de aplicativo vinculados às colunas em um conjunto de resultados, como seus endereços, comprimentos e tipos de dados C.  
  
-   **Descritor de linha de implementação (IRD).** Contém informações sobre as colunas em um conjunto de resultados, como seus tipos de dados SQL, comprimentos e nulidade.  
  
 Quatro descritores (um preenchendo cada função) são alocados automaticamente quando uma declaração é alocada. Estes são conhecidos como *descritores alocados automaticamente* e estão sempre associados a essa afirmação. Os aplicativos também podem alocar descritores com **SQLAllocHandle**. Estes são conhecidos como *descritores explicitamente alocados.* Eles são alocados em uma conexão e podem ser associados a uma ou mais declarações sobre essa conexão para cumprir o papel de um APD ou ARD nessas declarações.  
  
 A maioria das operações no ODBC pode ser realizada sem o uso explícito de descritores pelo aplicativo. No entanto, os descritores fornecem um atalho conveniente para algumas operações. Por exemplo, suponha que um aplicativo queira inserir dados de dois conjuntos diferentes de buffers. Para usar o primeiro conjunto de buffers, ele chamaria repetidamente **SQLBindParameter** para vinculá-los aos parâmetros em uma instrução **INSERT** e, em seguida, executar a instrução. Para usar o segundo conjunto de buffers, ele repetiria este processo. Alternativamente, ele poderia configurar vinculações para o primeiro conjunto de buffers em um descritor e para o segundo conjunto de buffers em outro descritor. Para alternar entre os conjuntos de vinculações, o aplicativo simplesmente ligaria **sqlsetstmtAttr** e associaria o descritor correto com a declaração como a APD.  
  
 Para obter mais informações sobre descritores, consulte [Tipos de Descritores](../../../odbc/reference/develop-app/types-of-descriptors.md).
