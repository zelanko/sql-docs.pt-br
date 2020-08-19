---
description: Aplicativos personalizados
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56829c72264ba128554af0534e8a6bfa16254142
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429388"
---
# <a name="custom-applications"></a>Aplicativos personalizados
Os aplicativos personalizados normalmente executam uma tarefa específica para alguns DBMSs. Por exemplo, um aplicativo pode recuperar dados de um único DBMS e gerar um relatório ou pode transferir dados entre vários DBMSs. O que esses aplicativos têm em comum é que esses DBMSs são conhecidos antes que o aplicativo seja escrito e seja improvável de mudar ao longo da vida útil do aplicativo.  
  
 O aplicativo personalizado, portanto, requer pouca ou nenhuma interoperabilidade. O desenvolvedor do aplicativo pode escolher um único driver para cada DBMS e codificar diretamente para esses drivers. O aplicativo pode conter com segurança o código específico do driver para explorar os recursos desses drivers e pode até fazer chamadas para a API do banco de dados nativo para usar a funcionalidade não suportada pelo ODBC.  
  
 A principal preocupação de interoperabilidade da maioria dos aplicativos personalizados é se os DBMS de destino serão alterados no futuro. Nesse caso, esse processo pode ser simplificado escrevendo-se mais código interoperável para começar. No entanto, essa alteração de DBMS é rara e geralmente envolve uma grande quantidade de trabalho. Por isso, os desenvolvedores de aplicativos personalizados raramente optam por aumentar a interoperabilidade às custas da funcionalidade; Normalmente, eles optam por recodificar essa funcionalidade quando alteram DBMSs.
