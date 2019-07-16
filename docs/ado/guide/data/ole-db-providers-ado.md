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
ms.openlocfilehash: 7e86375639d875f5cfec21705af47c005afd901e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924751"
---
# <a name="ole-db-providers-ado"></a>Provedores OLE DB (ADO)
OLE DB define um conjunto de interfaces COM para fornecer aplicativos com acesso uniforme a dados armazenados em várias fontes de informação. Essa abordagem permite que uma fonte de dados compartilhar seus dados por meio de interfaces que dão suporte a quantidade de funcionalidade do DBMS apropriada para a fonte de dados. Por design, a arquitetura de alto desempenho do banco de dados OLE baseia-se em seu uso de um modelo flexível e baseada em componente de serviços. Em vez de ter um número prescrito de camadas intermediárias entre o aplicativo e os dados, OLE DB requer somente à medida que muitos componentes como são necessários para realizar uma tarefa em particular.  
  
 Por exemplo, suponha que um usuário deseja executar uma consulta. Considere os seguintes cenário:  
  
-   Os dados residem em um banco de dados relacional para o qual atualmente, existe um driver ODBC, mas nenhum provedor OLE DB nativo: O aplicativo usa ADO para se comunicar com o provedor OLE DB para ODBC, que, em seguida, carrega o driver ODBC apropriado. O driver passa a instrução SQL para o DBMS, que recupera os dados.  
  
-   Os dados residem no Microsoft SQL Server para o qual há um provedor OLE DB nativo: O aplicativo usa ADO para comunicar diretamente com o provedor OLE DB para Microsoft SQL Server. Não há intermediários são necessários.  
  
-   Os dados residem no Microsoft Exchange Server, para que não há um provedor OLE DB, mas que não expõe um mecanismo para processar as consultas SQL: O aplicativo usa o ADO para se comunicar com o provedor OLE DB para o Microsoft Exchange e chama um componente de processador de consulta de OLE DB para lidar com a consulta.  
  
-   Os dados residem no sistema de arquivos NTFS Microsoft na forma de documentos: Dados são acessados por meio de um provedor OLE DB nativo em Microsoft Indexing Service, que indexa o conteúdo e propriedades de documentos no sistema de arquivos para permitir pesquisas eficientes de conteúdo.  
  
 Em todos os exemplos anteriores, o aplicativo pode consultar os dados. As necessidades do usuário são atendidas com um número mínimo de componentes. Em cada caso, componentes adicionais são usados somente se necessário, e apenas os componentes necessários são invocados. Esse carregamento por demanda dos componentes reutilizáveis e compartilháveis contribui muito para alto desempenho quando o OLE DB é usado.  
  
 Provedores se enquadram em duas categorias: àqueles que fornecem dados e aqueles fornecendo serviços. Um provedor de dados possui seus próprios dados e a expõe em formato de tabela para seu aplicativo. Um provedor de serviço encapsula um serviço, produzindo e consumindo dados, aumentando os recursos em seus aplicativos do ADO. Um provedor de serviços também pode ser ainda mais definido como um componente de serviço, que deve trabalhar em conjunto com outros provedores de serviços ou componentes.  
  
 ADO fornece uma consistente interface de nível mais alto para os vários provedores OLE DB.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Provedores de Dados](../../../ado/guide/data/data-providers.md)  
  
-   [Provedores de serviços e componentes](../../../ado/guide/data/service-providers-and-components.md)
