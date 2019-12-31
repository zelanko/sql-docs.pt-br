---
title: Arquitetura de cliente e XML do lado do servidor (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7f84e7ee16f945b5556c1ced480ac09070460d77
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247083"
---
# <a name="architecture-of-client-side-and-server-side-xml-formatting-sqlxml-40"></a>Arquitetura de formatação XML no lado do cliente e no lado do servidor (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A ilustração a seguir mostra a arquitetura de formatação XML no lado do servidor.  
  
 ![Arquitetura de formatação XML no lado do servidor.](../../../relational-databases/sqlxml/formatting/media/serversidexml.gif "Arquitetura de formatação XML no lado do servidor.")  
  
 Neste exemplo, o comando especificado no cliente é enviado ao servidor. O servidor gera um documento XML e o retorna ao cliente. Nesse caso, o servidor tem uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Com a formatação XML no lado do servidor, você pode usar o provedor SQLXMLOLEDB ou o provedor SQLOLEDB.  O provedor SQLXMLOLEDB usa Sqlxml4.dll que é incluído no SQLXML 4.0. Quando você usa o provedor SQLOLEDB, por padrão obtém a funcionalidade do SQLXML fornecida pela Sqlxmlx.dll, incluída com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows ou MDAC (Microsoft Data Access Components) 2.6 ou posterior. Para usar Sqlxml4. dll com SQLOLEDB, você deve definir a Propriedade Version do SQLXML como "SQLXML. 4.0" no objeto de conexão SQLOLEDB. Em todo caso, o servidor gera o documento XML e o envia ao cliente.  
  
> [!NOTE]  
>  As consultas e os diagramas de atualização XPath são analisados no cliente. Para obter a funcionalidade do diagrama de atualização ou do modelo XPath no SQLXML 4.0, use Sqlxml4.dll.  
  
 A ilustração a seguir mostra a arquitetura da formatação XML no lado do cliente.  
  
 ![Arquitetura de formatação XML no lado do cliente.](../../../relational-databases/sqlxml/formatting/media/clientsidexml.gif "Arquitetura de formatação XML no lado do cliente.")  
  
 Neste exemplo, o cliente usa o provedor SQLXMLOLEDB. Na cadeia de conexão, a propriedade Provedor de Dados deve ser definida como SQLOLEDB. (Esse é o único valor aceito no SQLXML 4,0.) O comando executado no cliente é enviado ao servidor. O conjunto de linhas gerado no servidor é enviado ao cliente. A formatação do documento XML do conjunto de linhas é executada no cliente.  
  
 No SQLXML 4.0, tanto o provedor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) como o SQLOLEDB podem ser usados como o provedor de dados. Você pode acessar potencialmente qualquer fonte de dados. Contanto que a consulta retorne um único conjunto de linhas, a transformação XML pode ser aplicada no cliente.  
  
  
