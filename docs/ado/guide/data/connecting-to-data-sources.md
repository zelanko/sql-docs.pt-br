---
title: Conectar-se a fontes de dados | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 000302715e7ce7d3a8ae53f06d61f54e98cbd883
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925793"
---
# <a name="connecting-to-data-sources"></a>Conectando-se a fontes de dados
ADO **Conexão** objeto representa uma sessão exclusiva com uma fonte de dados, incluindo um arquivo de texto delimitado por vírgula, um armazenamento de arquivos ou um DBMS. No caso de um sistema de banco de dados cliente/servidor, a conexão ADO pode ser uma conexão de rede reais para o servidor.  
  
 O **Conexão** objeto oferece suporte a vários [propriedades e métodos](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md) para especificar as configurações de conexão, abrindo e fechando conexões, criar e executar comandos na fonte de dados e fornecendo informações sobre o design de fonte de dados na forma de conjuntos de linhas de esquema, etc. Dependendo da funcionalidade compatível com o provedor, algumas coleções, métodos ou propriedades de um **Conexão** objeto pode não estar disponível.  
  
 Você pode se conectar a uma fonte de dados usando um **Conexão** do objeto ou usando uma **Recordset** objeto.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Usando um objeto Connection](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [Usando um objeto Recordset](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [Criando uma cadeia de conexão](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [Especificando propriedades de conexão](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [Controlar transações](../../../ado/guide/data/controlling-transactions-ado.md)
