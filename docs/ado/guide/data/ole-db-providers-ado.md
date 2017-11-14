---
title: Provedores OLE DB (ADO) | Microsoft Docs
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
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ef1c85f55928c266fb88f1639d5ccd53450fe59
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="ole-db-providers-ado"></a>Provedores OLE DB (ADO)
OLE DB define um conjunto de interfaces para fornecer aplicativos acesso padronizado aos dados armazenados em fontes diferentes de informações. Essa abordagem permite que uma fonte de dados compartilhar seus dados por meio de interfaces que oferecem suporte a quantidade de funcionalidade DBMS apropriada para a fonte de dados. Por design, a arquitetura de alto desempenho do OLE DB é baseada em seu uso de um modelo de serviços flexível baseado em componente. Em vez de um número prescrito de camadas intermediárias entre o aplicativo e os dados, OLE DB requer apenas que vários componentes que são necessários para realizar uma tarefa específica.  
  
 Por exemplo, suponha que um usuário deseja executar uma consulta. Considere os seguintes cenário:  
  
-   Os dados residem em um banco de dados relacional para o qual atualmente existe um driver ODBC, mas nenhum provedor OLE DB nativo: O aplicativo usa ADO para se comunicar com o provedor OLE DB para ODBC, que, em seguida, carrega o driver ODBC apropriado. O driver passa a instrução SQL para o DBMS, que recupera os dados.  
  
-   Os dados residem no Microsoft SQL Server para o qual há um provedor OLE DB nativo: O aplicativo usa ADO para se comunicar diretamente com o provedor OLE DB do Microsoft SQL Server. Nenhum intermediários são necessários.  
  
-   Os dados residem no Microsoft Exchange Server, para que não há um provedor OLE DB, mas que não expõe um mecanismo para processar as consultas SQL: O aplicativo usa o ADO para se comunicar com o provedor OLE DB para o Microsoft Exchange e chama um processador de consulta de banco de dados OLE componente para lidar com a consulta.  
  
-   Os dados residem no sistema de arquivos NTFS Microsoft na forma de documentos: os dados são acessados usando um provedor OLE DB nativo em Microsoft Indexing Service, que indexa o conteúdo e as propriedades de documentos no sistema de arquivos para habilitar conteúdo eficiente pesquisas.  
  
 Em todos os exemplos anteriores, o aplicativo pode consultar os dados. Necessidades do usuário são atendidas com um número mínimo de componentes. Em cada caso, os componentes adicionais são usados somente se necessário e somente os componentes necessários são invocados. Esse carregamento por demanda de componentes reutilizáveis e compartilháveis bastante contribui para alto desempenho quando o OLE DB é usado.  
  
 Provedores se enquadram em duas categorias: aqueles fornecendo dados e aqueles fornecendo serviços. Um provedor de dados possui seus próprios dados e expõe em formato tabular para seu aplicativo. Um provedor de serviço encapsula um serviço, produzindo e consumo de dados, aumentando os recursos em seus aplicativos do ADO. Um provedor de serviços também pode ser definido posteriormente como um componente de serviço, que deve trabalhar em conjunto com outros provedores de serviços ou componentes.  
  
 ADO fornece uma consistente interface de nível superior para vários provedores OLE DB.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Provedores de Dados](../../../ado/guide/data/data-providers.md)  
  
-   [Provedores de serviços e componentes](../../../ado/guide/data/service-providers-and-components.md)

