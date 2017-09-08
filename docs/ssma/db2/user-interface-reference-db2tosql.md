---
title: "Referência da Interface de usuário (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 98ecc4ff-9416-48a2-af0f-86852cf69dab
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b19bd52df094e13cadb042208cc42fb8da1a418c
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="user-interface-reference-db2tosql"></a>Referência da Interface de usuário (DB2ToSQL)
Esta seção inclui tópicos de ajuda para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) para DB2.  
  
## <a name="in-this-section"></a>Nesta seção  
A tabela a seguir lista as caixas de diálogo do SSMA:  
  
|||  
|-|-|  
|Tópico|Description|  
|[Avançado seleção de objetos &#40; DB2ToSQL &#41;](../../ssma/db2/advanced-object-selection-db2tosql.md)|Use o **avançado objeto selecione** caixa de diálogo para localizar objetos de banco de dados usando os critérios de filtro e, em seguida, marque ou desmarque esses objetos.|  
|[Relatório de avaliação &#40; DB2ToSQL &#41;](../../ssma/db2/assessment-report-db2tosql.md)|Use o relatório de avaliação para exibir os resultados da conversão de DB2 objetos para [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe e para estimar o tempo e a complexidade de uma migração para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Conectar-se ao banco de dados DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)|Use o **conectar ao DB2** caixa de diálogo para se conectar ao banco de dados DB2 que você deseja migrar.|  
|[Conectar ao SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/connect-to-sql-server-db2tosql.md)|Use o **conectar ao SQL Server** caixa de diálogo para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] aos quais você deseja migrar.|  
|[Relatório de migração de dados &#40; DB2ToSQL &#41;](../../ssma/db2/data-migration-report-db2tosql.md)|Exibe os resultados da migração de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Configurações de migração de dados](http://msdn.microsoft.com/en-us/573e673e-a194-4cb2-9aba-aaac6e1a225c)|Use o **configurações de migração de dados estendido** guia para criar consultas personalizadas para a migração de dados.|  
|[Editar mapeamento de tipo de &#40; DB2ToSQL &#41;](../../ssma/db2/edit-type-mapping-db2tosql.md)|Use o **novo mapeamento de tipo** ou **editar mapeamento de tipo** caixas de diálogo para criar ou modificar o mapeamento de tipos de dados entre bancos de dados de origem e de destino e objetos de banco de dados.|  
|[Configurações globais &#40; Editor de &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/global-settings-editor-db2tosql.md)|Use a página do Editor do **configurações globais** caixa de diálogo Configurar opções do editor de código.|  
|[Global configurações &#40; caixas de diálogo &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/global-settings-dialogs-db2tosql.md)|Use a página de caixas de diálogo do **configurações globais** caixa de diálogo para definir configurações de aviso e de caixa de diálogo padrão.|  
|[Configurações globais &#40; Registro em log &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/global-settings-logging-db2tosql.md)|Use a página de registro em log do **configurações globais** caixa de diálogo para configurar o log.|  
|[Global configurações &#40; a janela de saída &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/global-settings-output-window-db2tosql.md)|Use o **configurações globais** caixa de diálogo para definir as preferências para o SSMA para interface de usuário do DB2.|  
|[Novo projeto &#40; DB2ToSQL &#41;](../../ssma/db2/new-project-db2tosql.md)|Use o **novo projeto** caixa de diálogo para criar um novo SSMA para projeto de DB2.|  
|[Configurações de projeto &#40; Conversão de &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)|Use a página de conversão do **configurações de projeto** caixa de diálogo para especificar como o SSMA para DB2 converte funções e variáveis globais.|  
|[Configurações de projeto &#40; Interface gráfica do usuário &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-gui-db2tosql.md)|Use a página de GUI do **configurações de projeto** caixa de diálogo para especificar a quantidade de dados aparece no **dados** guia.|  
|[Configurações de projeto &#40; Migração de &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-migration-db2tosql.md)|Use a página de migração do **configurações de projeto** caixa de diálogo para personalizar como o SSMA para DB2 migra dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Configurações de projeto &#40; Sincronização &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)|Use a página de sincronização do **configurações de projeto** caixa de diálogo para personalizar como o SSMA para DB2 cria ou altera migrados objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Configurações de projeto &#40; Carregando objetos do sistema &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md)|Use a página carregar objetos do sistema do **configurações de projeto** caixa de diálogo para especificar qual sistema DB2 objetos SSMA converte e carrega em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Configurações de projeto &#40; Mapeamento de tipo de &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)|Use a página mapeamento de tipo do **configurações de projeto** caixa de diálogo para especificar os mapeamentos de tipo de padrão para todos os bancos de dados e objetos de banco de dados em SSMA para projeto de DB2.|  
|[Atualização do banco de dados &#40; DB2ToSQL &#41;](../../ssma/db2/refresh-from-database-db2tosql.md)|Use o **de atualização do banco de dados** caixa de diálogo para selecionar objetos para atualização do banco de dados DB2.|  
|[Salvar metadados &#40; DB2ToSQL &#41;](../../ssma/db2/save-metadata-db2tosql.md)|O **salvar metadados** caixa de diálogo aparece quando você salvar um projeto que falta metadados.|  
  
## <a name="see-also"></a>Consulte também  
[Guia de Introdução com o SSMA para DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
[Migrando bancos de dados do DB2 para SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

