---
description: Tipos de drivers
title: Tipos de drivers | Microsoft Docs
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
ms.openlocfilehash: 4ae3ab2b0172e97a221b446107ccbf4b6ae4eb7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476290"
---
# <a name="types-of-drivers"></a>Tipos de drivers
Os drivers ODBC podem ser classificados da seguinte maneira:  
  
-   **ODBC de 32 bits 2.**  
     ** _x_ driver** um driver de 32 bits que:  
  
    -   Exporta somente as funções ODBC *2. x* .  
  
    -   Exibe o comportamento do ODBC *2. x* para alterações comportamentais.  
  
-   **ISO e abrir o driver em conformidade com o grupo** Um driver de 32 bits que:  
  
    -   Exporta todas as funções documentadas nos documentos Open Group ou ISO CLI. Isso incluirá algumas funções que são preteridas no ODBC.  
  
    -   Exibe o comportamento do ODBC 3,0 para alterações comportamentais.  
  
    -   Não percorre necessariamente o Gerenciador de driver ODBC 3,0.  
  
-   **Driver ODBC 3,0** Um driver de 32 bits que:  
  
    -   Exporta somente as funções que estão em ODBC 3,0 menos funções preteridas.  
  
    -   É capaz de exibir o comportamento do ODBC *2. x* ou o comportamento do ODBC 3,0 com relação às alterações comportamentais, com base no atributo de ambiente SQL_ATTR_APP_ODBC_VERSION.  
  
-   **ODBC 3,5 (ou posterior) Driver ANSI** Um driver de 32 bits que:  
  
    -   Exporta somente as funções que estão em ODBC 3,5 menos funções preteridas.  
  
    -   É capaz de exibir o comportamento do ODBC *2. x* ou o comportamento do ODBC 3,0 ou o comportamento do ODBC 3,5 em relação às alterações comportamentais, com base no atributo de ambiente SQL_ATTR_APP_ODBC_VERSION.  
  
-   **Driver Unicode do ODBC 3,5 (ou posterior)** Um driver de 32 bits que:  
  
    -   Dá suporte a todos os recursos de um driver ANSI do ODBC 3,5.  
  
    -   Exporta as versões Unicode de todas as APIs de cadeia de caracteres ODBC.  
  
    -   Pode armazenar e processar dados Unicode na fonte de dados.  
  
> [!NOTE]  
>  drivers ODBC de 16 bits não funcionarão diretamente com o Gerenciador de driver ODBC *3. x* . No entanto, é possível que drivers de 16 bits funcionem com o Gerenciador de driver ODBC 2,0, que é então conversões mais tarde para o Gerenciador de driver *3. x* .
