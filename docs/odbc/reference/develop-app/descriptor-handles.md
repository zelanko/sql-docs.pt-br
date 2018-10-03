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
manager: craigg
ms.openlocfilehash: 3aa085cc0a098f557ca7a8cbddcd787a178b79d0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711604"
---
# <a name="descriptor-handles"></a>Identificadores de descritor
Um *descritor* é uma coleção de metadados que descrevem os parâmetros de uma instrução SQL ou as colunas de um conjunto de resultados, como visto pelo aplicativo ou driver (também conhecido como o *implementação*). Portanto, pode preencher um descritor de qualquer um dos quatro funções:  
  
-   **Parâmetro APD (descritor aplicativo).** Contém informações sobre os buffers de aplicativo associados aos parâmetros em uma instrução SQL, como seus endereços, tamanhos e tipos de dados C.  
  
-   **Descritor de parâmetro de implementação (IPD).** Contém informações sobre os parâmetros em uma instrução SQL, como seus tipos de dados SQL, comprimentos e nulidade.  
  
-   **Descritor de linha de aplicativo (descartar).** Contém informações sobre os buffers do aplicativo associado para as colunas em um conjunto de resultados, como seus endereços, tamanhos e tipos de dados C.  
  
-   **Descritor de linha de implementação (IRD).** Contém informações sobre as colunas em um conjunto de resultados, como seus tipos de dados SQL, comprimentos e nulidade.  
  
 Descritores de quatro (um preenchimento de cada função) são alocados automaticamente quando uma instrução é alocada. Eles são conhecidos como *alocado automaticamente descritores* e sempre estão associadas essa instrução. Aplicativos também podem alocar descritores com **SQLAllocHandle**. Eles são conhecidos como *alocado explicitamente descritores*. Eles são alocados em uma conexão e podem ser associados uma ou mais instruções sobre essa conexão para atender a função de um APD ou descartar essas instruções.  
  
 A maioria das operações em ODBC podem ser executadas sem o uso explícito de descritores de pelo aplicativo. No entanto, os descritores de fornecem um atalho prático para algumas operações. Por exemplo, suponha que um aplicativo quiser inserir dados de dois conjuntos diferentes de buffers. Para usar o primeiro conjunto de buffers, ele poderia chamar repetidamente **SQLBindParameter** vinculá-las para os parâmetros em um **inserir** instrução e, em seguida, execute a instrução. Para usar o segundo conjunto de buffers, ele repetiria esse processo. Como alternativa, ele poderia configurar associações para o primeiro conjunto de buffers em um descritor de e para o segundo conjunto de buffers no descritor de outro. Para alternar entre os conjuntos de associações, o aplicativo simplesmente chamaria **SQLSetStmtAttr** e associar o descritor correto com a instrução como APD.  
  
 Para obter mais informações sobre descritores, consulte [tipos de descritores](../../../odbc/reference/develop-app/types-of-descriptors.md).
