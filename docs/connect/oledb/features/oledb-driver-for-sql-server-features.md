---
title: Driver do OLE DB para recursos do SQL Server | Microsoft Docs
description: OLE DB Driver para recursos do SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 5cbc52f29aa0bfc6c60d9f8b7cb47b138c11b561
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612351"
---
# <a name="ole-db-driver-for-sql-server-features"></a>Driver do OLE DB para recursos do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Além de expor os recursos da (anteriormente Microsoft) Data Access componentes WDAC (Windows), OLE DB Driver para SQL Server também implementa vários outros recursos para expor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] funcionalidade.  
  
## <a name="in-this-section"></a>Nesta seção    
 [Usando o espelhamento de banco de dados](../../oledb/features/using-database-mirroring.md)  
 Discute como OLE DB Driver para SQL Server dá suporte ao uso de bancos de dados espelhados, que é a capacidade de manter uma cópia ou espelho, de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados em um servidor em espera.  
  
 [Executando operações assíncronas](../../oledb/features/performing-asynchronous-operations.md)  
 Discute como OLE DB Driver para SQL Server oferece suporte a operações assíncronas, que é a capacidade de retornar imediatamente sem bloqueio no thread de chamada.  
  
 [Usando MARS &#40;Multiple Active Result Sets&#41;](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 Discute como OLE DB Driver para SQL Server oferece suporte a vários conjuntos de resultados ativos (MARS). Os MARS permitem executar e receber vários conjuntos de resultados por meio de uma única conexão de banco de dados.  
  
 [Usando tipos de dados XML](../../oledb/features/using-xml-data-types.md)  
 Discute como OLE DB Driver para SQL Server dá suporte ao tipo de dados XML, que é um tipo de dados com base em XML que pode ser usado como um tipo de coluna, tipo de variável, tipo de parâmetro ou tipo de retorno da função.  
  
 [Usando tipos definidos pelo usuário](../../oledb/features/using-user-defined-types.md)  
 Discute como OLE DB Driver para SQL Server oferece suporte a User-Defined tipos (UDT), que estende o sistema de tipos SQL, permitindo armazenar objetos e estruturas de dados personalizadas em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados.  
  
 [Usando tipos de valor grande](../../oledb/features/using-large-value-types.md)  
 Discute como OLE DB Driver para SQL Server oferece suporte a tipos de dados de valor grande, que são tipos de dados de objeto grande (LOB).  
  
 [Alterando senhas programaticamente](../../oledb/features/changing-passwords-programmatically.md)  
 Discute como OLE DB Driver para SQL Server oferece suporte à manipulação de senhas expiradas para que as senhas agora podem ser alteradas no cliente sem o envolvimento do administrador.  
  
 [Trabalhando com isolamento de instantâneo](../../oledb/features/working-with-snapshot-isolation.md)  
 Discute como OLE DB Driver para SQL Server oferece suporte a melhoria do controle de versão de linha que melhora o desempenho do banco de dados, evitando cenários de bloqueio de leitor / gravador.  
  
 [Trabalhando com notificações de consulta](../../oledb/features/working-with-query-notifications.md)  
 Discute como o OLE DB Driver para SQL Server oferece suporte à notificação do consumidor na modificação do conjunto de linhas.  
  
 [Executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md)  
 Discute como OLE DB Driver para SQL Server oferece suporte a operações de cópia em massa que permitem a transferência de grandes quantidades de dados dentro ou fora de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabela ou exibição.  
  
 [Usando criptografia sem validação](../../oledb/features/using-encryption-without-validation.md)  
 Discute como usar o OLE DB Driver para SQL Server para criptografar dados enviados ao servidor sem validar o certificado.  
  
 [Parâmetros com valor de tabela &#40;Driver do OLE DB para SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 Discute o Driver OLE DB para o suporte do SQL Server para os parâmetros com valor de tabela.  
  
 [Tipos de dados CLR grandes definidos pelo usuário](../../oledb/features/large-clr-user-defined-types.md)  
 Aborda o suporte a UDTs CLR (Common Language Runtime) grandes.  
  
 [Suporte a FILESTREAM](../../oledb/features/filestream-support.md)  
 Discute o Driver do OLE DB para o suporte do SQL Server para o recurso FILESTREAM aprimorado.  
  
 [Nome da entidade de serviço &#40;SPN&#41; suporte em conexões de cliente](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 Aborda como o suporte a SPNs (nomes da entidade de serviço) foi estendido para possibilitar autenticação mútua em todos os protocolos.  
  
 [Suporte às colunas esparsas no Driver do OLE DB para SQL Server](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 Discute o Driver do OLE DB para o suporte do SQL Server para colunas esparsas.  
  
 [Aprimoramentos de data e hora](../../oledb/features/date-and-time-improvements.md)  
 Aborda o suporte adicionado para o Driver do OLE DB para SQL Server para os tipos de dados de data e hora.  
  
 [Descoberta de metadados](../../oledb/features/metadata-discovery.md)  
 Discute melhorias de descoberta de metadados que foram feitas no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Suporte ao UTF-16 no Driver do OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 Discute uma alteração no comportamento apresentada no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Se você fornecer um buffer de comprimento fixo ao associar um coluna de resultados ou parâmetro de saída e se o **wchar** caractere gravado no buffer antes da finalização do caractere é um ponto de código alternativo alto de um par substituto e se o próximo **wchar** caractere é um ponto de código alternativo baixo, OLE DB Driver para SQL Server não adicionará o ponto de código alternativo alto ao buffer.  
  
 [Suporte ao Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastre](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 Discute como seu aplicativo pode ser configurado para aproveitar a recuperação de desastres de alta disponibilidade, recursos adicionados [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Acessar informações de diagnóstico nos logs de eventos estendidos](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Discute os aprimoramentos Driver OLE DB para SQL Server e o rastreamento de dados que fornece acesso a informações de diagnóstico no buffer de anel e o log de XEvents.  
  
 [Suporte ao Driver do OLE DB para SQL Server para LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 Discute o Driver OLE DB para o suporte do SQL Server para o recurso LocalDB.  
  
## <a name="see-also"></a>Consulte também  
 [Driver do OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)      
 [Tópicos de instruções do OLE DB](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [Instalação do Driver do OLE DB para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
