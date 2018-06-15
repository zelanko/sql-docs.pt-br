---
title: Aplicativos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9475bc17948e2146493cade0f884cac8885eea62
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908381"
---
# <a name="custom-applications"></a>Aplicativos personalizados
Aplicativos personalizados normalmente executam uma tarefa específica para alguns DBMSs. Por exemplo, um aplicativo pode recuperar dados de um único DBMS e gerar um relatório, ou ele pode transferir dados entre vários DBMSs. O que esses aplicativos têm em comum é que essas DBMSs são conhecidos antes que o aplicativo é escrito e são improváveis de ser alterados durante a vida útil do aplicativo.  
  
 Portanto, o aplicativo personalizado requer interoperabilidade de pouca ou nenhuma. O desenvolvedor do aplicativo pode escolher um único driver para cada DBMS e o código diretamente esses drivers. O aplicativo com segurança pode conter código específico do driver para explorar os recursos desses drivers e pode até mesmo fazer chamadas para a API de banco de dados nativo para usar a funcionalidade não tem suporte pelo ODBC.  
  
 A preocupação principal de interoperabilidade da maioria dos aplicativos personalizada é se o destino DBMSs será alterado no futuro. Nesse caso, esse processo pode ser simplificado, escrevendo código mais interoperável começar com. No entanto, essa alteração de DBMSs é rara e geralmente envolve uma grande quantidade de trabalho. Por isso, os desenvolvedores de aplicativos personalizados raramente optar por aumentar interoperabilidade às custas da funcionalidade; eles normalmente escolher recodificar essa funcionalidade quando alteram DBMSs.
