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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 445fe3a0b87e6ad8e35dbc585981d874f8e357bf
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256951"
---
# <a name="types-of-drivers"></a>Tipos de drivers
Drivers ODBC podem ser classificados da seguinte maneira:  
  
-   **2 de ODBC de 32 bits.**  
     **_x_ Driver** driver de 32 bits que:  
  
    -   Exporta somente ODBC 2 *. x* funções.  
  
    -   Exibe o ODBC 2. *x* comportamento para alterações de comportamento.  
  
-   **ISO e o Driver compatível com o grupo aberto** driver de 32 bits que:  
  
    -   Exporta todas as funções que estão documentadas nos documentos Open Group ou a CLI do ISO. Isso inclui algumas das funções que foram preteridas no ODBC.  
  
    -   Exibe o comportamento de ODBC 3.0 para alterações de comportamento.  
  
    -   Não necessariamente passa através do Gerenciador de Driver ODBC 3.0.  
  
-   **Driver ODBC 3.0** driver de 32 bits que:  
  
    -   Exporta as funções apenas que estão no ODBC 3.0 menos funções preteridas.  
  
    -   É capaz de que apresentam o ODBC 2. *x* comportamento ou o comportamento de ODBC 3.0 com relação às alterações comportamentais, com base no atributo SQL_ATTR_APP_ODBC_VERSION ambiente.  
  
-   **Driver ODBC 3.5 (ou posterior) ANSI** driver de 32 bits que:  
  
    -   Exporta somente funções de ODBC 3.5 menos funções preteridas.  
  
    -   É capaz de que apresentam o ODBC 2. *x* comportamento ou o comportamento de ODBC 3.0 ou o comportamento de ODBC 3.5 em relação às alterações comportamentais, com base no atributo SQL_ATTR_APP_ODBC_VERSION ambiente.  
  
-   **Driver ODBC 3.5 (ou posterior) Unicode** driver de 32 bits que:  
  
    -   Dá suporte a todos os recursos de um driver de ODBC 3.5 ANSI.  
  
    -   Exporta as versões Unicode da cadeia de caracteres ODBC todas as APIs.  
  
    -   Pode armazenar e processar dados de Unicode na fonte de dados.  
  
> [!NOTE]  
>  drivers ODBC de 16 bits não funciona diretamente com o ODBC 3. *x* Gerenciador de Driver. No entanto, é possível que os drivers de 16 bits trabalhar com o Gerenciador de Driver ODBC 2.0, que é subsequentemente conversões até a 3. *x* Gerenciador de Driver.
