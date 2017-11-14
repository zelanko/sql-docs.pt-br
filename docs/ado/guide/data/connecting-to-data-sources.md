---
title: Conectando-se a fontes de dados | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [ADO]
ms.assetid: 82770486-37bd-4c90-885f-6817a7c77ad7
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 47aa7f058db324c7388801ae6a391b6c0c24ae1d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-to-data-sources"></a>Conectando-se a fontes de dados
ADO **Conexão** objeto representa uma sessão exclusiva com uma fonte de dados, incluindo um DBMS, um repositório de arquivo ou um arquivo de texto delimitado por vírgula. No caso de um sistema de banco de dados cliente/servidor, a conexão ADO pode ser uma conexão de rede reais para o servidor.  
  
 O **Conexão** objeto oferece suporte a vários [propriedades e métodos](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md) para especificar configurações de conexão, abertura e fechamento de conexões, criar e executar comandos em relação à fonte de dados e fornecer informações sobre o design de fonte de dados na forma de conjuntos de linhas de esquema, etc. Dependendo da funcionalidade com suporte do provedor, algumas coleções, métodos ou propriedades de um **Conexão** objeto pode não estar disponível.  
  
 Você pode se conectar a uma fonte de dados usando um **Conexão** do objeto ou usando um **registros** objeto.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Usando um objeto Connection](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [Usando um objeto Recordset](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [Criando uma cadeia de conexão](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [Especificando propriedades de conexão](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [Controle de transações](../../../ado/guide/data/controlling-transactions-ado.md)

