---
title: As Classes fundamentais AMO | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [AMO]
- AMO, database objects
- AMO, server objects
- Analysis Management Objects, server objects
- database objects [AMO]
- Analysis Management Objects, database objects
- AMO, data sources
- Analysis Management Objects, data sources
ms.assetid: 440e9287-53a2-4db3-9481-1d2ceb6e5b5a
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ee31478a526dad385d9721256beebc4324cadb60
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118549"
---
# <a name="amo-fundamental-classes"></a>Classes fundamentais AMO
  As classes fundamentais são o ponto de partida para o trabalho com o AMO (Objetos de Gerenciamento de Análise). Por meio dessas classes você estabelece o ambiente para o resto dos objetos que serão usados em seu aplicativo. As classes fundamentais incluem os seguintes objetos: <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource> e <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
 A ilustração a seguir mostra o relacionamento das classes explicadas neste tópico.  
  
 ![As Classes fundamentais AMO](../../../analysis-services/dev-guide/media/amo-fundamentalclasses.gif "as Classes fundamentais AMO")  
  
  
  
##  <a name="ServerObjects"></a> Objetos de servidor  
 Adicionalmente, você terá acesso aos seguintes métodos:  
  
-   Gerenciamento de conexão: Connect, Disconnect, Reconnect e GetConnectionState.  
  
-   Gerenciamento de transação: BeginTransaction, CommitTransaction e RollbackTransaction.  
  
-   Backup e restauração.  
  
-   Execução de DDL: Execute, CancelCommand, SendXmlaRequest, StartXmlaRequest.  
  
-   Gerenciamento de metadados: UpdateObjects e Validate.  
  
 Para conectar a um servidor, você precisa de uma cadeia de conexão padrão, como usado no ADOMD.NET e no OLEDB. Para obter mais informações, consulte <xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>. O nome do servidor pode ser especificado como uma cadeia de conexão sem o uso de um formato de cadeia de conexão.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Server> em <xref:Microsoft.AnalysisServices>.  
  
##  <a name="DatabaseObjects"></a> Objetos de banco de dados  
 Para trabalhar com um objeto <xref:Microsoft.AnalysisServices.Database> em seu aplicativo, obtenha uma instância do banco de dados da coleção de bancos de dados do servidor pai. Para criar um banco de dados, adicione um objeto <xref:Microsoft.AnalysisServices.Database> a uma coleção de bancos de dados de servidor e atualize a nova instância para o servidor. Para excluir um banco de dados, descarte o objeto <xref:Microsoft.AnalysisServices.Database> usando seu próprio método Drop.  
  
 Você pode fazer backup dos bancos de dados usando o método BackUp (a partir do objeto de <xref:Microsoft.AnalysisServices.Database> ou a partir do objeto <xref:Microsoft.AnalysisServices.Server>), mas ele só poderá ser restaurado a partir do objeto <xref:Microsoft.AnalysisServices.Server> com o método Restore.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Database> em <xref:Microsoft.AnalysisServices>.  
  
##  <a name="DSandDSV"></a> Objetos DataSource e DataSourceView  
 As fontes de dados são gerenciadas por meio de <xref:Microsoft.AnalysisServices.DataSourceCollection> da classe do banco de dados. Uma instância de <xref:Microsoft.AnalysisServices.DataSource> pode ser criada usando o método Add de um objeto <xref:Microsoft.AnalysisServices.DataSourceCollection>. Uma instância de <xref:Microsoft.AnalysisServices.DataSource> pode ser excluída usando o método Remove de um objeto <xref:Microsoft.AnalysisServices.DataSourceCollection>.  
  
 Os objetos <xref:Microsoft.AnalysisServices.DataSourceView> são gerenciados a partir do objeto <xref:Microsoft.AnalysisServices.DataSourceViewCollection> na classe do banco de dados.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.DataSource> e <xref:Microsoft.AnalysisServices.DataSourceView> em <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices>   
 [Introdução às Classes AMO](amo-classes-introduction.md)   
 [Programando objetos AMO fundamentais](programming-amo-fundamental-objects.md)  
  
  