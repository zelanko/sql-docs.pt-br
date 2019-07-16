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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067471"
---
# <a name="custom-applications"></a>Aplicativos personalizados
Aplicativos personalizados normalmente executam uma tarefa específica para alguns DBMSs. Por exemplo, um aplicativo pode recuperar dados de um DBMS único e gerar um relatório, ou ele pode transferir dados entre vários DBMSs. O que esses aplicativos têm em comum é que esses DBMSs são conhecidos antes que o aplicativo é escrito e são improváveis de ser alterado durante a vida útil do aplicativo.  
  
 O aplicativo personalizado, portanto, requer pouca ou nenhuma interoperabilidade. O desenvolvedor do aplicativo pode escolher um único driver para cada DBMS e o código diretamente para esses drivers. O aplicativo com segurança pode conter código específico do driver para explorar os recursos desses drivers e pode até fazer chamadas para a API de banco de dados nativo para usar a funcionalidade não tem suporte pelo ODBC.  
  
 A preocupação de interoperabilidade principal da maioria dos aplicativos personalizados é se o destino DBMSs será alterado no futuro. Nesse caso, esse processo pode ser simplificado ao escrever código mais interoperável para começar. No entanto, essa alteração de DBMSs é rara e geralmente envolve uma grande quantidade de trabalho. Por causa disso, os desenvolvedores de aplicativos personalizados raramente optar por aumentar a interoperabilidade em detrimento da funcionalidade; eles geralmente escolher recodificar essa funcionalidade ao alterar os DBMSs.
