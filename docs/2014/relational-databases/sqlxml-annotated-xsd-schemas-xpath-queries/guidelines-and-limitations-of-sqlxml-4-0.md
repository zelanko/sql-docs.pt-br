---
title: Diretrizes e limitações do SQLXML 4.0 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
ms.assetid: fe433d30-90a1-421e-85c6-af13294dc18d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a9dbc7ebb66852d4fc97c36e9508870e6724160b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180436"
---
# <a name="guidelines-and-limitations-of-sqlxml-40"></a>Diretrizes e limitações do SQLXML 4.0
  Lembre-se do seguinte ao trabalhar com SQLXML 4.0:  
  
-   O XML retornado como um resultado de consulta não é validado com relação ao esquema de mapeamento que gerou o XML.  
  
-   O SQLXML 4.0 inclui PROGIDs dependentes e independentes de versão. É recomendável que todos os aplicativos de produção usem os PROGIDs dependentes de versão. Isto é especialmente importante porque o SQLXML 4.0 não é completamente compatível com versões anteriores. O uso de PROGIDs dependentes de versão o protege de possíveis falhas de produção quando você instala versões mais recentes. De versão para versão, o comportamento do programa pode ser alterado por uma série de motivos, como correções de bug, possíveis alterações de design etc. O uso de PROGIDs dependentes de versão o protege de falhas inesperadas quando você instala versões mais recentes. Com PROGIDs dependentes de versão, quando você instala uma versão mais recente, seu aplicativo continua a operar sem falha. Se você decidir alterar PROGIDs dependentes de versão anteriores e usar PROGIDs dependentes de versão recentes em uma versão mais recente, deverá testar seu aplicativo antes de colocá-lo em produção. Por exemplo, aplicativos que usam os PROGIDs independentes de versão podem falhar neste cenário:  
  
     Você está executando um aplicativo que usa SQLXML 4.0 e os PROGIDs dependentes de versão, e decide instalar outro programa de software. Esse programa pode instalar uma versão anterior do SQLXML. Seu aplicativo pode falhar, pois os PROGIDS independentes de versão do seu aplicativo agora apontam para a versão mais antiga do SQLXML, o que pode ou não possuir o recurso SQL XML que seu aplicativo está usando.  
  
-   Se por algum motivo você não deseja usar o provedor SQLXMLOLEDB e, em vez disso deseja usar o SQLOLEDB provedor para os recursos do SQLXML, defina as **SQLXML Version** propriedade como "SQLXML.4.0".  
  
  
