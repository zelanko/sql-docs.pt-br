---
title: Provedores OLE DB (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3f4f1d4efed51a8f9e3b5eaf3bd4a2c7f385e75
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613804"
---
# <a name="ole-db-providers-ado"></a>Provedores OLE DB (ADO)
OLE DB define um conjunto de interfaces COM para fornecer aplicativos com acesso uniforme a dados armazenados em várias fontes de informação. Essa abordagem permite que uma fonte de dados compartilhar seus dados por meio de interfaces que dão suporte a quantidade de funcionalidade do DBMS apropriada para a fonte de dados. Por design, a arquitetura de alto desempenho do banco de dados OLE baseia-se em seu uso de um modelo flexível e baseada em componente de serviços. Em vez de ter um número prescrito de camadas intermediárias entre o aplicativo e os dados, OLE DB requer somente à medida que muitos componentes como são necessários para realizar uma tarefa em particular.  
  
 Por exemplo, suponha que um usuário deseja executar uma consulta. Considere os seguintes cenário:  
  
-   Os dados residem em um banco de dados relacional para o qual atualmente, existe um driver ODBC, mas nenhum provedor OLE DB nativo: O aplicativo usa ADO para se comunicar com o provedor OLE DB para ODBC, que, em seguida, carrega o driver ODBC apropriado. O driver passa a instrução SQL para o DBMS, que recupera os dados.  
  
-   Os dados residem no Microsoft SQL Server para o qual há um provedor OLE DB nativo: O aplicativo usa ADO para comunicar diretamente com o provedor OLE DB para Microsoft SQL Server. Não há intermediários são necessários.  
  
-   Os dados residem no Microsoft Exchange Server, para que não há um provedor OLE DB, mas que não expõe um mecanismo para processar as consultas SQL: O aplicativo usa ADO para se comunicar com o provedor OLE DB para o Microsoft Exchange e chama um processador de consulta de banco de dados OLE componente para lidar com a consulta.  
  
-   Os dados residem no sistema de arquivos NTFS Microsoft na forma de documentos: dados são acessados por meio de um provedor OLE DB nativo em Microsoft Indexing Service, que indexa o conteúdo e propriedades de documentos no sistema de arquivos para permitir eficiente ao conteúdo pesquisas.  
  
 Em todos os exemplos anteriores, o aplicativo pode consultar os dados. As necessidades do usuário são atendidas com um número mínimo de componentes. Em cada caso, componentes adicionais são usados somente se necessário, e apenas os componentes necessários são invocados. Esse carregamento por demanda dos componentes reutilizáveis e compartilháveis contribui muito para alto desempenho quando o OLE DB é usado.  
  
 Provedores se enquadram em duas categorias: àqueles que fornecem dados e aqueles fornecendo serviços. Um provedor de dados possui seus próprios dados e a expõe em formato de tabela para seu aplicativo. Um provedor de serviço encapsula um serviço, produzindo e consumindo dados, aumentando os recursos em seus aplicativos do ADO. Um provedor de serviços também pode ser ainda mais definido como um componente de serviço, que deve trabalhar em conjunto com outros provedores de serviços ou componentes.  
  
 ADO fornece uma consistente interface de nível mais alto para os vários provedores OLE DB.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Provedores de Dados](../../../ado/guide/data/data-providers.md)  
  
-   [Provedores de serviços e componentes](../../../ado/guide/data/service-providers-and-components.md)
