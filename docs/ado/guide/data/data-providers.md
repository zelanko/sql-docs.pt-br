---
title: Provedores de dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 30d1e1515ed3e84640fe1ca004cb7cbf4383ce97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718720"
---
# <a name="data-providers"></a>Provedores de Dados
Provedores de dados representam as diversas fontes de dados, como bancos de dados SQL, arquivos indexados sequenciais, planilhas, repositórios de documentos e arquivos de email. Provedores de expõem dados uniformemente usando uma abstração comum chamada conjunto de linhas.  
  
 ADO é poderoso e flexível, porque ele pode se conectar a qualquer um dos vários provedores de dados diferentes e ainda expor o mesmo modelo de programação, independentemente dos recursos específicos de qualquer provedor determinado. No entanto, como cada provedor de dados é exclusivo, como o seu aplicativo interage com o ADO variam por provedor de dados.  
  
 Por exemplo, recursos e capacidades do provedor OLE DB para SQL Server, que é usado para acessar bancos de dados do Microsoft SQL Server, são consideravelmente diferentes do Microsoft OLE DB Provider para publicação de Internet, que é usado para acessar o arquivo armazena em um servidor Web.
