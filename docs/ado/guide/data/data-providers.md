---
title: Provedores de dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddd360c49c3cbd10b76dc39e6c161a523a93b1bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-providers"></a>Provedores de Dados
Provedores de dados representam diversas fontes de dados, como bancos de dados SQL, arquivos indexados sequencial, planilhas, repositórios de documentos e arquivos de email. Provedores de expõem dados uniformemente usando uma abstração comum, chamada conjunto de linhas.  
  
 O ADO é poderoso e flexível porque ele pode se conectar a qualquer um dos vários provedores de dados diferentes e ainda expor o mesmo modelo de programação, independentemente dos recursos específicos de qualquer provedor determinado. No entanto, como cada provedor de dados é exclusivo, como seu aplicativo interage com o ADO variam por provedor de dados.  
  
 Por exemplo, as capacidades e recursos do provedor OLE DB para SQL Server, que é usado para acessar bancos de dados do Microsoft SQL Server, são muito diferentes do Microsoft OLE DB Provider para publicação de Internet, que é usado para acessar o arquivo armazena em um servidor Web.
