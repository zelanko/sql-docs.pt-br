---
title: Criando um aplicativo de provedor do SQL Server Native Client OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, application creation
- applications [SQL Server Native Client]
- OLE DB, creating applications
ms.assetid: f3ae6815-f32d-4913-a1a2-2ba2f20cfd88
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 769c151f6b115065b62b2b3b4f7d9fc61b408463
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426791"
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>Criando um aplicativo provedor OLE DB do SQL Server Native Client
  Criando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicativo do provedor OLE DB do Native Client envolve estas etapas:  
  
1.  Estabelecimento de uma conexão a uma fonte de dados.  
  
2.  Execução de um comando.  
  
3.  Processamento dos resultados.  
  
> [!NOTE]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário manter credenciais, criptografe-as com [cryptoAPI Win32](http://go.microsoft.com/fwlink/?LinkId=9504).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Estabelecendo uma conexão com uma fonte de dados](establishing-a-connection-to-a-data-source.md)  
  
-   [Executando um comando](executing-a-command.md)  
  
-   [Processando resultados](processing-results.md)  
  
-   [Sobre propriedades OLE DB](about-ole-db-properties.md)  
  
-   [Usando a cláusula OUTPUT com OLE DB no SQL Server Native Client](using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
