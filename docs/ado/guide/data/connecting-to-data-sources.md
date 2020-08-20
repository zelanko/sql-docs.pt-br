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
ms.openlocfilehash: 78d7395adfb30dbf78d88baadabc42ede409f47a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453638"
---
# <a name="connecting-to-data-sources"></a>Conectando-se a fontes de dados
Um objeto de **conexão** ADO representa uma sessão exclusiva com uma fonte de dados, incluindo um DBMS, um repositório de arquivos ou um arquivo de texto delimitado por vírgula. No caso de um sistema de banco de dados cliente/servidor, a conexão ADO pode ser uma conexão de rede real com o servidor.  
  
 O objeto de **conexão** dá suporte a várias [Propriedades e métodos](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md) para especificar configurações de conexão, abrir e fechar conexões, criar e executar comandos na fonte de dados e fornecer informações sobre o design da fonte de dados subjacente na forma de conjuntos de linhas de esquema, etc. Dependendo da funcionalidade suportada pelo provedor, algumas coleções, métodos ou propriedades de um objeto de **conexão** podem não estar disponíveis.  
  
 Você pode se conectar a uma fonte de dados usando um objeto de **conexão** ou um objeto **Recordset** .  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Usando um objeto Connection](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [Usando um objeto Recordset](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [Criando uma cadeia de conexão](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [Especificando propriedades de conexão](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [Controle de transações](../../../ado/guide/data/controlling-transactions-ado.md)
