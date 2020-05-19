---
title: Recursos de SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a516578a0d72028ec8543d136f571ea62d7520b6
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707238"
---
# <a name="sql-server-native-client-features"></a>Recursos do SQL Server Native Client
  Além de expor os recursos do WDAC (Windows (anteriormente Microsoft) Data Access Components), o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client também implementa vários outros recursos para expor a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Alteração de comportamento do driver ODBC ao lidar com conversões de caracteres](odbc-driver-behavior-change-when-handling-character-conversions.md)  
 Discute uma alteração de comportamento a partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client.  
  
 [Usando o espelhamento de banco de dados](using-database-mirroring.md)  
 Discute como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client dá suporte ao uso de bancos de dados espelhados, que é a capacidade de manter uma cópia, ou espelho, de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados em um servidor em espera.  
  
 [Executando operações assíncronas](performing-asynchronous-operations.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte a operações assíncronas, o que possibilita o retorno imediato sem bloqueio no thread que fez a chamada.  
  
 [Usando MARS &#40;Multiple Active Result Sets&#41;](using-multiple-active-result-sets-mars.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte a MARS (vários conjuntos de resultados ativos). Os MARS permitem executar e receber vários conjuntos de resultados por meio de uma única conexão de banco de dados.  
  
 [Usando tipos de dados XML](using-xml-data-types.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte ao tipo de dados XML, um tipo de dados baseado em XML que pode ser usado como um tipo de coluna, um tipo de variável, um tipo de parâmetro ou um tipo de retorno de função.  
  
 [Usando tipos definidos pelo usuário](using-user-defined-types.md)  
 Discute como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client dá suporte a UDT (tipos definidos pelo usuário), que estende o sistema de tipos SQL, permitindo que você armazene objetos e estruturas de dados personalizadas em um banco de dado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 [Usando tipos de valor grande](using-large-value-types.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte a tipos de dados de valor grande, que são tipos de dados LOB (objeto binário grande).  
  
 [Alterando senhas programaticamente](changing-passwords-programmatically.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte ao tratamento de senhas expiradas de forma que as senhas agora possam ser alteradas no cliente sem o envolvimento do administrador.  
  
 [Trabalhando com isolamento de instantâneo](working-with-snapshot-isolation.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte ao aprimoramento do controle de versão de linha que melhora o desempenho do banco de dados ao evitar cenários de bloqueio de leitor/gravador.  
  
 [Trabalhando com notificações de consulta](working-with-query-notifications.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte à notificação do consumidor na modificação do conjunto de linhas.  
  
 [Executando operações de cópia em massa](performing-bulk-copy-operations.md)  
 Discute como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client dá suporte a operações de cópia em massa que permitem a transferência de grandes quantidades de dados para dentro ou para fora de uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabela ou exibição.  
  
 [Usando criptografia sem validação](using-encryption-without-validation.md)  
 Aborda como usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para criptografar dados enviados para o servidor sem validar o certificado.  
  
 [Os parâmetros com valor de tabela &#40;SQL Server Native Client&#41;](table-valued-parameters-sql-server-native-client.md)  
 Aborda o suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client aos parâmetros com valor de tabela.  
  
 [Tipos de dados CLR grandes definidos pelo usuário](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 Aborda o suporte a UDTs CLR (Common Language Runtime) grandes.  
  
 [Suporte a FILESTREAM](filestream-support.md)  
 Discute [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o suporte de cliente nativo para o recurso de fluxo de recursos avançado.  
  
 [Suporte a SPN &#40;Nome da Entidade de Serviço&#41; em conexões com o cliente](service-principal-name-spn-support-in-client-connections.md)  
 Aborda como o suporte a SPNs (nomes da entidade de serviço) foi estendido para possibilitar autenticação mútua em todos os protocolos.  
  
 [Suporte a colunas esparsas no SQL Server Native Client](sparse-columns-support-in-sql-server-native-client.md)  
 Aborda o suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a colunas esparsas.  
  
 [Melhorias de data e hora](date-and-time-improvements.md)  
 Aborda o suporte adicionado ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para os novos tipos de dados de data e hora.  
  
 [Descoberta de metadados](metadata-discovery.md)  
 Discute melhorias de descoberta de metadados que foram feitas no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Suporte a UTF-16 no SQL Server Native Client 11.0](utf-16-support-in-sql-server-native-client-11-0.md)  
 Discute uma alteração no comportamento apresentada no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Se você fornecer um buffer de comprimento fixo ao associar um resultado de coluna ou parâmetro de saída e se o caractere `wchar` gravado no buffer antes da finalização do caractere for um ponto de código alternativo alto de um par alternativo, e se o próximo caractere `wchar` for um ponto de código alternativo baixo, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não adicionará o ponto de código alternativo alto ao buffer.  
  
 [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 Aborda como seu aplicativo pode ser configurado para aproveitar os recursos de alta disponibilidade e de recuperação de desastre adicionados no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Acessando informações de diagnóstico no log de eventos estendidos](accessing-diagnostic-information-in-the-extended-events-log.md)  
 Discute os aprimoramentos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o rastreamento de dados que fornece acesso a informações de diagnóstico no buffer de anel e no log de XEvents.  
  
 [Suporte do SQL Server Native Client para LocalDB](sql-server-native-client-support-for-localdb.md)  
 Discute o suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ao recurso LocalDB.  
  
## <a name="see-also"></a>Consulte Também  
 [Programação de SQL Server Native Client](../sql-server-native-client-programming.md)   
 [Tópicos de instruções sobre ODBC](../../native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Tópicos de instruções sobre OLE DB](../../native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [Instalando o SQL Server Native Client](../applications/installing-sql-server-native-client.md)  
  
  
