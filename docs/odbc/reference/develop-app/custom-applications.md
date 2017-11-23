---
title: Aplicativos personalizados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fe974d13b438cdb7fe010a35621665557cf2af8d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="custom-applications"></a>Aplicativos personalizados
Aplicativos personalizados normalmente executam uma tarefa específica para alguns DBMSs. Por exemplo, um aplicativo pode recuperar dados de um único DBMS e gerar um relatório, ou ele pode transferir dados entre vários DBMSs. O que esses aplicativos têm em comum é que essas DBMSs são conhecidos antes que o aplicativo é escrito e são improváveis de ser alterados durante a vida útil do aplicativo.  
  
 Portanto, o aplicativo personalizado requer interoperabilidade de pouca ou nenhuma. O desenvolvedor do aplicativo pode escolher um único driver para cada DBMS e o código diretamente esses drivers. O aplicativo com segurança pode conter código específico do driver para explorar os recursos desses drivers e pode até mesmo fazer chamadas para a API de banco de dados nativo para usar a funcionalidade não tem suporte pelo ODBC.  
  
 A preocupação principal de interoperabilidade da maioria dos aplicativos personalizada é se o destino DBMSs será alterado no futuro. Nesse caso, esse processo pode ser simplificado, escrevendo código mais interoperável começar com. No entanto, essa alteração de DBMSs é rara e geralmente envolve uma grande quantidade de trabalho. Por isso, os desenvolvedores de aplicativos personalizados raramente optar por aumentar interoperabilidade às custas da funcionalidade; eles normalmente escolher recodificar essa funcionalidade quando alteram DBMSs.
