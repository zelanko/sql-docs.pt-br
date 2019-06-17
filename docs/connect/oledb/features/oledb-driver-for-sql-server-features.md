---
title: Driver do OLE DB para recursos do SQL Server | Microsoft Docs
description: Recursos do OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 445345d39d5612fb543466900cee97d64a567d87
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800868"
---
# <a name="ole-db-driver-for-sql-server-features"></a>Recursos do OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Além de expor os recursos do WDAC [Windows (anteriormente Microsoft) Data Access Components], o OLE DB Driver for SQL Server também implementa vários outros recursos para expor a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção    
 [Usando o espelhamento de banco de dados](../../oledb/features/using-database-mirroring.md)  
 Aborda como o OLE DB Driver for SQL Server dá suporte ao uso de bancos de dados espelhados, o que possibilita manter uma cópia, ou um espelho, de um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um servidor em espera.  
  
 [Executando operações assíncronas](../../oledb/features/performing-asynchronous-operations.md)  
 Aborda como o OLE DB Driver for SQL Server dá suporte a operações assíncronas, o que possibilita o retorno imediato sem bloqueio no thread de chamada.  

[Como usar o Azure Active Directory](using-azure-active-directory.md)  
Discute os novos métodos de autenticação introduzidos no driver do OLE DB 18.2.1 que têm configurações padrão mais seguras e permitem a conexão com uma instância do banco de dados do SQL Azure usando uma identidade federada.

 [Usando MARS &#40;Multiple Active Result Sets&#41;](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 Discute como o Driver do OLE DB para SQL Server dá suporte a vários conjuntos de resultados ativos (MARS). Os MARS permitem executar e receber vários conjuntos de resultados por meio de uma única conexão de banco de dados.  
  
 [Usando tipos de dados XML](../../oledb/features/using-xml-data-types.md)  
 Aborda como o OLE DB Driver for SQL Server dá suporte ao tipo de dados XML, um tipo de dados baseado em XML que pode ser usado como um tipo de coluna, um tipo de variável, um tipo de parâmetro ou um tipo de retorno de função.  
  
 [Usando tipos definidos pelo usuário](../../oledb/features/using-user-defined-types.md)  
 Aborda como o OLE DB Driver for SQL Server dá suporte a UDTs (Tipos Definidos pelo Usuário), que estendem o sistema de tipos SQL permitindo que você armazene objetos e estruturas de dados personalizadas em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Usando tipos de valor grande](../../oledb/features/using-large-value-types.md)  
 Discute como o Driver do OLE DB para SQL Server dá suporte a tipos de dados de valor grande, que são tipos de dados de objeto grande (LOB).  
  
 [Alterando senhas programaticamente](../../oledb/features/changing-passwords-programmatically.md)  
 Aborda como o OLE DB Driver for SQL Server dá suporte ao tratamento de senhas expiradas, de forma que as senhas agora possam ser alteradas no cliente sem o envolvimento do administrador.  
  
 [Trabalhando com isolamento de instantâneo](../../oledb/features/working-with-snapshot-isolation.md)  
 Aborda como o OLE DB Driver for SQL Server dá suporte à melhoria do controle de versão de linha que melhora o desempenho do banco de dados prevenindo cenários de bloqueio de leitor/gravador.  
  
 [Trabalhando com notificações de consulta](../../oledb/features/working-with-query-notifications.md)  
 Discute como o Driver do OLE DB para SQL Server dá suporte à notificação de consumidor na modificação do conjunto de linhas.  
  
 [Executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md)  
 Aborda como o OLE DB Driver for SQL Server dá suporte a operações de cópia em massa que permitem a transferência de grandes quantidades de dados para dentro ou fora de uma tabela ou uma exibição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Usando criptografia sem validação](../../oledb/features/using-encryption-without-validation.md)  
 Discute como usar o Driver do OLE DB para SQL Server para criptografar dados enviados ao servidor sem validar o certificado.  
  
 [Parâmetros com valor de tabela &#40;OLE DB Driver for SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 Discute o Driver do OLE DB para o suporte do SQL Server para os parâmetros com valor de tabela.  
  
 [Tipos de dados CLR grandes definidos pelo usuário](../../oledb/features/large-clr-user-defined-types.md)  
 Aborda o suporte a UDTs CLR (Common Language Runtime) grandes.  
  
 [Suporte a FILESTREAM](../../oledb/features/filestream-support.md)  
 Discute o Driver do OLE DB para o suporte do SQL Server para o recurso FILESTREAM aprimorado.  
  
 [Suporte a SPN &#40;Nome da Entidade de Serviço&#41; em conexões de cliente](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 Aborda como o suporte a SPNs (nomes da entidade de serviço) foi estendido para possibilitar autenticação mútua em todos os protocolos.  
  
 [Suporte às colunas esparsas no Driver do OLE DB para SQL Server](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 Discute o Driver do OLE DB para o suporte do SQL Server para colunas esparsas.  
  
 [Aprimoramentos de data e hora](../../oledb/features/date-and-time-improvements.md)  
 Discute o suporte adicionado ao Driver do OLE DB para SQL Server para os tipos de dados de data e hora.  
  
 [Descoberta de metadados](../../oledb/features/metadata-discovery.md)  
 Discute melhorias de descoberta de metadados que foram feitas no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Suporte ao UTF-16 no Driver do OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 Discute uma alteração no comportamento apresentada no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Se você fornecer um buffer de comprimento fixo ao associar um resultado de coluna ou um parâmetro de saída e se o caractere **wchar** gravado no buffer antes do caractere de terminação for um ponto de código alternativo alto de um par alternativo e se o próximo caractere **wchar** for um ponto de código alternativo baixo, o OLE DB Driver for SQL Server não adicionará o ponto de código alternativo alto ao buffer.  
 
 [Suporte ao UTF-8 no OLE DB Driver for SQL Server](../../oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
 Discute o suporte para produtos de precauções de codificação e a configuração de servidor UTF-8 os usuários devem tomar ao trabalhar com dados codificados em UTF-8.
  
 [Suporte ao Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastre](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 Aborda como seu aplicativo pode ser configurado para aproveitar os recursos de alta disponibilidade e de recuperação de desastre adicionados no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Acessar informações de diagnóstico nos logs de eventos estendidos](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Aborda as melhorias ao OLE DB Driver for SQL Server e o rastreamento de dados que fornece acesso a informações de diagnóstico no buffer de anéis e no log de XEvents.  
  
 [Suporte ao Driver do OLE DB para SQL Server para LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 Discute o Driver do OLE DB para o suporte do SQL Server para o recurso LocalDB.  
  
## <a name="see-also"></a>Consulte Também  
 [OLE DB Driver for SQL Server](../../oledb/oledb-driver-for-sql-server.md)      
 [Tópicos de instruções do OLE DB](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [Instalação do Driver do OLE DB para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
