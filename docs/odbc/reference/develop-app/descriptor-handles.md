---
title: Identificadores de descritor | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 99b1b3dc2eabd38aea148ad5ba946d7dd0da857d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="descriptor-handles"></a>Identificadores de descritor
Um *descritor* é uma coleção de metadados que descrevem os parâmetros de uma instrução SQL ou as colunas do conjunto de resultados, como visto pelo aplicativo ou driver (também conhecido como o *implementação*). Portanto, pode preencher um descritor de qualquer um dos quatro funções:  
  
-   **Parâmetro APD (descritor aplicativo).** Contém informações sobre os buffers de aplicativo associada aos parâmetros em uma instrução SQL, como seus endereços, tamanhos e tipos de dados C.  
  
-   **Parâmetro IPD (descritor implementação).** Contém informações sobre os parâmetros em uma instrução SQL, como seus tipos de dados SQL, comprimento e nulidade.  
  
-   **Descritor de linha de aplicativo (descartar).** Contém informações sobre os buffers de aplicativo associados a colunas em um conjunto de resultados, como seus endereços, tamanhos e tipos de dados C.  
  
-   **Descritor de linha de implementação (IRD).** Contém informações sobre as colunas em um conjunto de resultados, como seus tipos de dados SQL, comprimento e nulidade.  
  
 Descritores de quatro (um preenchimento de cada função) são alocados automaticamente quando uma instrução é alocada. Eles são conhecidos como *alocados automaticamente descritores* e sempre estão associados essa instrução. Aplicativos também podem alocar descritores com **SQLAllocHandle**. Eles são conhecidos como *explicitamente alocada descritores*. Eles são alocados em uma conexão e podem ser associados uma ou mais instruções sobre essa conexão para atender a função de um APD ou descartar essas instruções.  
  
 A maioria das operações em ODBC podem ser executadas sem o uso explícito de descritores pelo aplicativo. No entanto, os descritores de fornecem um atalho prático para algumas operações. Por exemplo, suponha que um aplicativo que deseja inserir dados de dois conjuntos diferentes de buffers. Para usar o primeiro conjunto de buffers, poderia chamar repetidamente **SQLBindParameter** para associá-las para os parâmetros em uma **inserir** instrução e, em seguida, execute a instrução. Para usar o segundo conjunto de buffers, ele deve repetir esse processo. Como alternativa, ele pode configurar associações para o primeiro conjunto de buffers em um descritor e o segundo conjunto de buffers no descritor do outro. Para alternar entre os conjuntos de associações, o aplicativo poderia simplesmente chamar **SQLSetStmtAttr** e associar o descritor correto com a instrução como APD.  
  
 Para obter mais informações sobre descritores, consulte [tipos de descritores](../../../odbc/reference/develop-app/types-of-descriptors.md).

