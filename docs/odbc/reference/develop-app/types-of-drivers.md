---
title: Tipos de Drivers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
ms.assetid: 864c53c1-b68a-48b6-b6bc-5ecb520bb9dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de6d8e1473f127d28c69969e0fc298afd69d3023
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304867"
---
# <a name="types-of-drivers"></a>Tipos de drivers
Os drivers ODBC podem ser classificados da seguinte forma:  
  
-   **ODBC 2 de 32 bits.**  
     ** _x_ Driver** Um driver de 32 bits que:  
  
    -   Exporta apenas funções ODBC *2.x.*  
  
    -   Exibe o comportamento oDBC *2.x* para mudanças comportamentais.  
  
-   **Iso e Motorista compatível com grupo aberto** Um driver de 32 bits que:  
  
    -   Exporta todas as funções documentadas nos documentos CLI do Grupo Aberto ou ISO. Isso incluirá algumas das funções que são preteridas no ODBC.  
  
    -   Exibe o comportamento oDBC 3.0 para mudanças comportamentais.  
  
    -   Não necessariamente passa pelo Gerenciador de Driver ODBC 3.0.  
  
-   **Driver ODBC 3.0** Um driver de 32 bits que:  
  
    -   As exportações só funcionam em ODBC 3.0 menos funções depreciadas.  
  
    -   É capaz de exibir comportamento ODBC *2.x* ou comportamento ODBC 3.0 em relação a mudanças comportamentais, com base no SQL_ATTR_APP_ODBC_VERSION atributo do ambiente.  
  
-   **Driver ANSI ODBC 3.5 (ou posterior)** Um driver de 32 bits que:  
  
    -   As exportações só funcionam em ODBC 3,5 menos funções depreciadas.  
  
    -   É capaz de exibir comportamento ODBC *2.x* ou comportamento ODBC 3.0, ou comportamento ODBC 3.5 em relação a mudanças comportamentais, com base no atributo SQL_ATTR_APP_ODBC_VERSION ambiente.  
  
-   **Driver Unicode ODBC 3.5 (ou posterior)** Um driver de 32 bits que:  
  
    -   Suporta todos os recursos de um driver ODBC 3.5 ANSI.  
  
    -   Exporta versões Unicode de todas as APIs de seqüência de strings ODBC.  
  
    -   Pode armazenar e processar dados Unicode na fonte de dados.  
  
> [!NOTE]  
>  Os drivers ODBC de 16 bits não funcionarão diretamente com o Gerenciador de Driver ODBC *3.x.* No entanto, é possível que os drivers de 16 bits trabalhem com o Gerenciador de Driver 2.0 ODBC, que posteriormente se depara com o Driver Manager *3.x.*
