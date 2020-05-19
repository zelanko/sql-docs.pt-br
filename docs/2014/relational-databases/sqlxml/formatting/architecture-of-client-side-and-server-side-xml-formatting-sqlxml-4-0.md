---
title: Arquitetura da formatação XML do lado do cliente e do servidor (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], XML formatting architecture
- SQLOLEDB provider
- client-side XML formatting
- data providers [SQLXML], XML formatting architecture
- SQLNCLI, XML
- server-side XML formatting
- SQL Server Native Client, XML
- SQLXMLOLEDB Provider, XML formatting architecture
ms.assetid: 52440d9e-89fd-4c15-a008-a1ea99f41387
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: caebd8ecad5fe9a48745d10adff28cf2a68d6a1d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702920"
---
# <a name="architecture-of-client-side-and-server-side-xml-formatting-sqlxml-40"></a>Arquitetura de formatação XML no lado do cliente e no lado do servidor (SQLXML 4.0)
  A ilustração a seguir mostra a arquitetura de formatação XML no lado do servidor.  
  
 ![Arquitetura de formatação XML no lado do servidor.](../../../database-engine/dev-guide/media/serversidexml.gif "Arquitetura de formatação XML no lado do servidor.")  
  
 Neste exemplo, o comando especificado no cliente é enviado ao servidor. O servidor gera um documento XML e o retorna ao cliente. Nesse caso, o servidor tem uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Com a formatação XML no lado do servidor, você pode usar o provedor SQLXMLOLEDB ou o provedor SQLOLEDB.  O provedor SQLXMLOLEDB usa Sqlxml4.dll que é incluído no SQLXML 4.0. Quando você usa o provedor SQLOLEDB, por padrão obtém a funcionalidade do SQLXML fornecida pela Sqlxmlx.dll, incluída com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows ou MDAC (Microsoft Data Access Components) 2.6 ou posterior. Para usar Sqlxml4. dll com SQLOLEDB, você deve definir a Propriedade Version do SQLXML como "SQLXML. 4.0" no objeto de conexão SQLOLEDB. Em todo caso, o servidor gera o documento XML e o envia ao cliente.  
  
> [!NOTE]  
>  As consultas e os diagramas de atualização XPath são analisados no cliente. Para obter a funcionalidade do diagrama de atualização ou do modelo XPath no SQLXML 4.0, use Sqlxml4.dll.  
  
 A ilustração a seguir mostra a arquitetura da formatação XML no lado do cliente.  
  
 ![Arquitetura de formatação XML no lado do cliente.](../../../database-engine/dev-guide/media/clientsidexml.gif "Arquitetura de formatação XML no lado do cliente.")  
  
 Neste exemplo, o cliente usa o provedor SQLXMLOLEDB. Na cadeia de conexão, a propriedade Provedor de Dados deve ser definida como SQLOLEDB. (Esse é o único valor aceito no SQLXML 4,0.) O comando executado no cliente é enviado ao servidor. O conjunto de linhas gerado no servidor é enviado ao cliente. A formatação do documento XML do conjunto de linhas é executada no cliente.  
  
 No SQLXML 4.0, tanto o provedor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) como o SQLOLEDB podem ser usados como o provedor de dados. Você pode acessar potencialmente qualquer fonte de dados. Contanto que a consulta retorne um único conjunto de linhas, a transformação XML pode ser aplicada no cliente.  
  
  
