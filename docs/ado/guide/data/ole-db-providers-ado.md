---
description: Provedores OLE DB (ADO)
title: Provedores de OLE DB (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
author: rothja
ms.author: jroth
ms.openlocfilehash: 227c3ead2744c475a54f129078b5674587ae3849
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453118"
---
# <a name="ole-db-providers-ado"></a>Provedores OLE DB (ADO)
OLE DB define um conjunto de interfaces COM para fornecer aos aplicativos acesso uniforme aos dados armazenados em diversas fontes de informações. Essa abordagem permite que uma fonte de dados Compartilhe seus dados por meio das interfaces que dão suporte à quantidade de funcionalidade de DBMS apropriada à fonte de dados. Por design, a arquitetura de alto desempenho do OLE DB é baseada no uso de um modelo de serviços flexível baseado em componentes. Em vez de ter um número prescrito de camadas intermediárias entre o aplicativo e os dados, OLE DB requer apenas quantos componentes forem necessários para realizar uma tarefa específica.  
  
 Por exemplo, suponha que um usuário queira executar uma consulta. Considere os seguintes cenário:  
  
-   Os dados residem em um banco de dado relacional para o qual existe atualmente um driver ODBC, mas nenhum provedor de OLE DB nativo: o aplicativo usa o ADO para se comunicar com o provedor de OLE DB para ODBC, que então carrega o driver ODBC apropriado. O driver passa a instrução SQL para o DBMS, que recupera os dados.  
  
-   Os dados residem no Microsoft SQL Server para o qual há um provedor de OLE DB nativo: o aplicativo usa o ADO para se comunicar diretamente com o provedor de OLE DB para Microsoft SQL Server. Não são necessários intermediários.  
  
-   Os dados residem no Microsoft Exchange Server, para o qual há um provedor de OLE DB, mas que não expõe um mecanismo para processar consultas SQL: o aplicativo usa o ADO para se comunicar com o provedor de OLE DB para o Microsoft Exchange e chama um componente de processador de consulta OLE DB para lidar com a consulta.  
  
-   Os dados residem no sistema de arquivos NTFS da Microsoft na forma de documentos: os dados são acessados usando um provedor de OLE DB nativo sobre o serviço de indexação da Microsoft, que indexa o conteúdo e as propriedades de documentos no sistema de arquivos para permitir pesquisas de conteúdo eficientes.  
  
 Em todos os exemplos anteriores, o aplicativo pode consultar os dados. As necessidades do usuário são atendidas com um número mínimo de componentes. Em cada caso, componentes adicionais são usados apenas se necessário, e apenas os componentes necessários são invocados. Esse carregamento por demanda de componentes reutilizáveis e compartilháveis contribui muito para o alto desempenho quando OLE DB é usado.  
  
 Os provedores se enquadram em duas categorias: aquelas que fornecem dados e aqueles que fornecem serviços. Um provedor de dados possui seus próprios dados e os expõe em formato de tabela para seu aplicativo. Um provedor de serviços encapsula um serviço, produzindo e consumindo dados, aumentando os recursos em seus aplicativos ADO. Um provedor de serviços também pode ser definido como um componente de serviço, que deve funcionar em conjunto com outros provedores de serviços ou componentes.  
  
 O ADO fornece uma interface consistente e de nível superior para vários provedores de OLE DB.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Provedores de dados](../../../ado/guide/data/data-providers.md)  
  
-   [Provedores de serviços e componentes](../../../ado/guide/data/service-providers-and-components.md)
