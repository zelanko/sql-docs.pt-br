---
title: "Replica&#231;&#227;o do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicação [SQL Server], sobre"
  - "replicação [SQL Server]"
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
caps.latest.revision: 58
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 58
---
# Replica&#231;&#227;o do SQL Server
  A replicação é um conjunto de tecnologias para copiar e distribuir dados e objetos de um banco de dados para outro e, em seguida, sincronizar entre os bancos de dados para manter a consistência. Usando replicação, é possível distribuir dados para diferentes locais e para usuários remotos e móveis através de redes locais e de longa distância, conexões discadas, conexões sem-fio e a Internet.  
  
 A replicação transacional normalmente é usada em cenários de servidor para servidor que requerem alta taxa de transferência, incluindo: melhora da escalabilidade e disponibilidade; armazenamento de dados data warehouse e relatórios; integração de dados de vários sites; integração de dados heterogêneos e descarregamento de processamento em lote. A replicação de mesclagem é projetada principalmente para aplicativos móveis ou de servidor distribuído que possuem possíveis conflitos de dados. Os cenários comuns incluem: troca de dados com usuários móveis; aplicativos de POS (ponto de vendas) para o consumidor e integração de dados de vários sites. A replicação de instantâneo é usada para fornecer o conjunto inicial de dados para replicação transacional e de mesclagem. Ela também pode ser usada quando atualizações completas de dados forem apropriadas. Com esses três tipos de replicação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um sistema poderoso e flexível para sincronizar dados em sua empresa. A replicação para SQLCE 3.5 e SQLCE 4.0 tem suporte no [!INCLUDE[win8srv](../../includes/win8srv-md.md)] e no [!INCLUDE[win8](../../includes/win8-md.md)].  
  
 Como alternativa à replicação, você pode sincronizar bancos de dados por meio do Microsoft Sync Framework. O Sync Framework inclui componentes e uma API intuitiva e flexível que facilitam a sincronização entre os bancos de dados SQL Server, SQL Server Express, SQL Server Compact e SQL Azure. O Sync Framework também incluir classes que podem ser adaptadas para sincronização entre um banco de dados do SQL Server e qualquer outro banco de dados que seja compatível com o ADO.NET. Para obter a documentação detalhada dos componentes de sincronização de banco de dados do Sync Framework, consulte [Sincronizando bancos de dados](http://go.microsoft.com/fwlink/?LinkId=209079). Para obter uma visão geral do Sync Framework, consulte a [Central do desenvolvedor do Microsoft Sync Framework](http://go.microsoft.com/fwlink/?LinkId=209078). Para obter uma comparação entre o Sync Framework e Replicação de Mesclagem, consulte [Visão geral da sincronização de bancos de dados](http://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  
 **Procurar conteúdo por área**  
 ![Ícone de pasta de arquivos pequeno](../../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Novidades](../../relational-databases/replication/what-s-new-replication.md)  
  
 ![Ícone de pasta de arquivos pequeno](../../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Compatibilidade com versões anteriores](../../relational-databases/replication/replication-backward-compatibility.md)  
  
 ![Ícone de pasta de arquivos pequeno](../../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Recursos e tarefas de replicação](../../relational-databases/replication/replication-features-and-tasks.md)  
  
 ![Ícone de pasta de arquivos pequeno](../../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Referência técnica](../../relational-databases/replication/technical-reference-replication.md)  
  
  