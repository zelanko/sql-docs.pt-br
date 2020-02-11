---
title: Aplicativos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 240bdf074fbe7fd28f5aafff5c1bbab7651d0c71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067471"
---
# <a name="custom-applications"></a>Aplicativos personalizados
Os aplicativos personalizados normalmente executam uma tarefa específica para alguns DBMSs. Por exemplo, um aplicativo pode recuperar dados de um único DBMS e gerar um relatório ou pode transferir dados entre vários DBMSs. O que esses aplicativos têm em comum é que esses DBMSs são conhecidos antes que o aplicativo seja escrito e seja improvável de mudar ao longo da vida útil do aplicativo.  
  
 O aplicativo personalizado, portanto, requer pouca ou nenhuma interoperabilidade. O desenvolvedor do aplicativo pode escolher um único driver para cada DBMS e codificar diretamente para esses drivers. O aplicativo pode conter com segurança o código específico do driver para explorar os recursos desses drivers e pode até fazer chamadas para a API do banco de dados nativo para usar a funcionalidade não suportada pelo ODBC.  
  
 A principal preocupação de interoperabilidade da maioria dos aplicativos personalizados é se os DBMS de destino serão alterados no futuro. Nesse caso, esse processo pode ser simplificado escrevendo-se mais código interoperável para começar. No entanto, essa alteração de DBMS é rara e geralmente envolve uma grande quantidade de trabalho. Por isso, os desenvolvedores de aplicativos personalizados raramente optam por aumentar a interoperabilidade às custas da funcionalidade; Normalmente, eles optam por recodificar essa funcionalidade quando alteram DBMSs.
