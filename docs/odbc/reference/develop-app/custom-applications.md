---
title: Aplicações personalizadas | Microsoft Docs
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
ms.openlocfilehash: df00a748ee4d5e3a63b32c95449417a1057b58e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305277"
---
# <a name="custom-applications"></a>Aplicativos personalizados
Aplicativos personalizados normalmente executam uma tarefa específica para alguns DBMSs. Por exemplo, um aplicativo pode recuperar dados de um único DBMS e gerar um relatório, ou pode transferir dados entre vários DBMSs. O que esses aplicativos têm em comum é que esses DBMSs são conhecidos antes do aplicativo ser escrito e são improváveis de mudar ao longo da vida útil do aplicativo.  
  
 A aplicação personalizada requer, portanto, pouca ou nenhuma interoperabilidade. O desenvolvedor de aplicativos pode escolher um único driver para cada DBMS e codificar diretamente para esses drivers. O aplicativo pode conter com segurança o código específico do driver para explorar os recursos desses drivers e pode até mesmo fazer chamadas para a API de banco de dados nativo para usar funcionalidades não suportadas pelo ODBC.  
  
 A maior preocupação de interoperabilidade da maioria dos aplicativos personalizados é se o DBMSs de destino mudará no futuro. Se assim for, esse processo pode ser simplificado escrevendo mais código interoperável para começar. No entanto, tal mudança de DBMSs é rara e geralmente implica uma grande quantidade de trabalho. Por causa disso, os desenvolvedores de aplicativos personalizados raramente optam por aumentar a interoperabilidade em detrimento da funcionalidade; eles geralmente optam por recodificar essa funcionalidade quando mudam DBMSs.
