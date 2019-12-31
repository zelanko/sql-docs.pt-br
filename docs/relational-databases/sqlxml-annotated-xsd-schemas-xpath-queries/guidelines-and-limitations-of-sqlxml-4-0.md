---
title: Diretrizes e limitações do SQLXML 4.0
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
ms.assetid: fe433d30-90a1-421e-85c6-af13294dc18d
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ba2e7438a9084d7ad2d4f8edee9564236ecbadd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257245"
---
# <a name="guidelines-and-limitations-of-sqlxml-40"></a>Diretrizes e limitações do SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Lembre-se do seguinte ao trabalhar com SQLXML 4.0:  
  
-   O XML retornado como um resultado de consulta não é validado com relação ao esquema de mapeamento que gerou o XML.  
  
-   O SQLXML 4.0 inclui PROGIDs dependentes e independentes de versão. É recomendável que todos os aplicativos de produção usem os PROGIDs dependentes de versão. Isto é especialmente importante porque o SQLXML 4.0 não é completamente compatível com versões anteriores. O uso de PROGIDs dependentes de versão o protege de possíveis falhas de produção quando você instala versões mais recentes. De versão para versão, o comportamento do programa pode ser alterado por uma série de motivos, como correções de bug, possíveis alterações de design etc. O uso de PROGIDs dependentes de versão o protege de falhas inesperadas quando você instala versões mais recentes. Com PROGIDs dependentes de versão, quando você instala uma versão mais recente, seu aplicativo continua a operar sem falha. Se você decidir alterar PROGIDs dependentes de versão anteriores e usar PROGIDs dependentes de versão recentes em uma versão mais recente, deverá testar seu aplicativo antes de colocá-lo em produção. Por exemplo, aplicativos que usam os PROGIDs independentes de versão podem falhar neste cenário:  
  
     Você está executando um aplicativo que usa SQLXML 4.0 e os PROGIDs dependentes de versão, e decide instalar outro programa de software. Esse programa pode instalar uma versão anterior do SQLXML. Seu aplicativo pode falhar, pois os PROGIDS independentes de versão do seu aplicativo agora apontam para a versão mais antiga do SQLXML, o que pode ou não possuir o recurso SQL XML que seu aplicativo está usando.  
  
-   Se, por algum motivo, você não quiser usar o provedor SQLXMLOLEDB e, em vez disso, quiser usar o provedor SQLOLEDB para os recursos do SQLXML, defina a propriedade **versão do SQLXML** como "SQLXML. 4.0".  
  
  
