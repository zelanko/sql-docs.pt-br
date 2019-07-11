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
ms.openlocfilehash: 08c1c9b4338502f20e5f99885d371d713971aa38
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792697"
---
# <a name="types-of-drivers"></a>Tipos de drivers
Drivers ODBC podem ser classificados da seguinte maneira:  
  
-   **2 de ODBC de 32 bits.**  
     **_x_ Driver** driver de 32 bits que:  
  
    -   Exporta somente ODBC *2.x* funções.  
  
    -   Exibe o ODBC *2.x* comportamento para alterações de comportamento.  
  
-   **ISO e o Driver compatível com o grupo aberto** driver de 32 bits que:  
  
    -   Exporta todas as funções que estão documentadas nos documentos Open Group ou a CLI do ISO. Isso inclui algumas das funções que foram preteridas no ODBC.  
  
    -   Exibe o comportamento de ODBC 3.0 para alterações de comportamento.  
  
    -   Não necessariamente passa através do Gerenciador de Driver ODBC 3.0.  
  
-   **Driver ODBC 3.0** driver de 32 bits que:  
  
    -   Exporta as funções apenas que estão no ODBC 3.0 menos funções preteridas.  
  
    -   É capaz de apresentando ODBC *2.x* comportamento ou o comportamento de ODBC 3.0 com relação às alterações comportamentais, com base no atributo SQL_ATTR_APP_ODBC_VERSION ambiente.  
  
-   **Driver ODBC 3.5 (ou posterior) ANSI** driver de 32 bits que:  
  
    -   Exporta somente funções de ODBC 3.5 menos funções preteridas.  
  
    -   É capaz de apresentando ODBC *2.x* comportamento ou o comportamento de ODBC 3.0 ou o comportamento de ODBC 3.5 em relação às alterações comportamentais, com base no atributo SQL_ATTR_APP_ODBC_VERSION ambiente.  
  
-   **Driver ODBC 3.5 (ou posterior) Unicode** driver de 32 bits que:  
  
    -   Dá suporte a todos os recursos de um driver de ODBC 3.5 ANSI.  
  
    -   Exporta as versões Unicode da cadeia de caracteres ODBC todas as APIs.  
  
    -   Pode armazenar e processar dados de Unicode na fonte de dados.  
  
> [!NOTE]  
>  drivers ODBC de 16 bits não funciona diretamente com o ODBC *3.x* Gerenciador de Driver. No entanto, é possível que os drivers de 16 bits trabalhar com o Gerenciador de Driver ODBC 2.0, que é subsequentemente conversões até a *3.x* Gerenciador de Driver.
