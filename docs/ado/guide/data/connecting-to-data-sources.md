---
description: Conectando-se a fontes de dados
title: Conectando-se a fontes de dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 82770486-37bd-4c90-885f-6817a7c77ad7
author: rothja
ms.author: jroth
ms.openlocfilehash: 1de885a14dd2647df08ae6245f64a629d706796d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806320"
---
# <a name="connecting-to-data-sources"></a>Conectando-se a fontes de dados
Um objeto de **conexão** ADO representa uma sessão exclusiva com uma fonte de dados, incluindo um DBMS, um repositório de arquivos ou um arquivo de texto delimitado por vírgula. No caso de um sistema de banco de dados cliente/servidor, a conexão ADO pode ser uma conexão de rede real com o servidor.  
  
 O objeto de **conexão** dá suporte a várias [Propriedades e métodos](../../reference/ado-api/connection-object-properties-methods-and-events.md) para especificar configurações de conexão, abrir e fechar conexões, criar e executar comandos na fonte de dados e fornecer informações sobre o design da fonte de dados subjacente na forma de conjuntos de linhas de esquema, etc. Dependendo da funcionalidade suportada pelo provedor, algumas coleções, métodos ou propriedades de um objeto de **conexão** podem não estar disponíveis.  
  
 Você pode se conectar a uma fonte de dados usando um objeto de **conexão** ou um objeto **Recordset** .  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Usar um objeto Connection](./using-a-connection-object.md)  
  
-   [Usar um objeto Recordset](./using-a-recordset-object.md)  
  
-   [Criando uma cadeia de conexão](./creating-a-connection-string.md)  
  
-   [Especificar propriedades de conexão](./specifying-connection-properties.md)  
  
-   [Controle de transações](./controlling-transactions-ado.md)