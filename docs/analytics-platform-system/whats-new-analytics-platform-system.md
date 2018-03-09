---
title: "O que há de novo no Analytics Platform System – um depósito de dados de expansão"
author: happynicolle
ms.author: nicw;barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Veja o que há de novo no Microsoft® Analytics Platform System, um aplicativo de expansão no local que hospeda MPP SQL Server Parallel Data Warehouse."
ms.date: 11/28/2016
ms.topic: article
ms.openlocfilehash: eeeb41045527e72856edfb8bdb40becc462bde07
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="whats-new-in-analytics-platform-system-2016-a-scale-out-mpp-data-warehouse"></a>O que há de novo no Analytics Platform System 2016, um data warehouse de MPP de expansão
Consulte o que há de novo no Microsoft® Analytics Platform System (APS) 2016, a atualização mais recente do dispositivo de um dispositivo de expansão no local que hospeda MPP SQL Server Parallel Data Warehouse. 

## <a name="sql-server-2016"></a>SQL Server 2016

APS 2016 é executado na versão mais recente do SQL Server 2016 e usa o nível de compatibilidade do banco de dados padrão 130.  SQL Server 2016 torna possível dar suporte a alguns dos novos recursos, como índices secundários para índices columnstore clusterizados e o Kerberos para PolyBase. 


## <a name="t-sql"></a>T-SQL
APS 2016 dá suporte a esses melhorias de compatibilidade do T-SQL.  Esses elementos de linguagem adicionais facilitam a migração do SQL Server e outras fontes de dados. 

- [Agrupamentos no nível de coluna SQL][] agora têm suporte além de agrupamentos do Windows.
- [Índices não clusterizados em índices columnstore clusterizados][] melhorar o desempenho de consultas que pesquisam valores específicos no índice columnstore clusterizado. 
- [SELECIONE... EM][] 
- [sp_spaceused()][] exibe o espaço em disco usado ou reservados em uma tabela ou banco de dados.
- [Tabelas largas][] suporte é o mesmo SQL Server 2016. O limite anterior de 32K para o tamanho de linha não existe mais. 

### <a name="data-types"></a>Tipos de dados

- [Varchar (max)][], [nvarchar (max)][] e [varbinary (max)][]. Esses tipos de dados LOB têm um tamanho máximo de 2 GB. Para carregar esses objetos de uso [utilitário bcp][]. Polybase e dwloader atualmente não suportam esses tipos de dados. 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [NUMÉRICO][] e tipos de dados DECIMAL.

### <a name="window-functions"></a>Funções de janela

- [ROWS ou RANGE][] na cláusula OVER da instrução SELECT.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

### <a name="security-functions"></a>Funções de segurança

- [CHECKSUM()][] e [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

### <a name="additional-functions"></a>Funções adicionais

- [NEWID)][]
- [RAND)][]

## <a name="polybasehadoop-enhancements"></a>Aprimoramentos de PolyBase/Hadoop

- Compatibilidade com Hortonworks HDP 2.4 e HDP 2.5
- Suporte a Kerberos por meio de credenciais no escopo do banco de dados
- Suporte de credencial com Blobs de armazenamento do Azure

## <a name="install-and-upgrade-enhancements"></a>Instalar e aprimoramentos de atualização

### <a name="enterprise-architecture-updates"></a>Atualizações de arquitetura empresarial
Atualizar seu dispositivo existente para APS 2016 instala o firmware mais recente e atualizações de driver, que incluem correções de segurança. 

Um novo dispositivo de HPE ou DELL inclui todas as atualizações mais recentes plus:

- Suporte de processador de geração mais recente (Broadwell)
- Atualizar para DIMMs DDR4
- Maior taxa de transferência do DIMM

### <a name="integration"></a>Integração

- Totalmente o suporte de nome de domínio qualificado (FQDN) possibilita configurar uma relação de confiança de domínio para o dispositivo. 
- Para usar o FQDN, você precisa fazer uma atualização completa e participar durante a atualização. 

### <a name="reduced-downtime"></a>Tempo de inatividade reduzido
Instalando ou atualizando para 2016 APS é mais rápido e requer menos tempo de inatividade de versões anteriores. Para reduzir o tempo de inatividade, a instalação ou atualização: 

 - Simplifica a aplicação de atualizações do WSUS usando uma imagem que contém todas as atualizações por meio de junho de 2016
 - Aplica-se as atualizações de segurança com as atualizações de firmware e driver
 - Coloca os hotfixes mais recentes e o utilitário de verificação de dispositivo (PAV) em sua aplicação para que eles fiquem prontos para instalar sem precisar baixá-los.


<!--MSDN references-->
[database compatibility level 130]:https://msdn.microsoft.com/library/bb510680.aspx
[Agrupamentos no nível de coluna SQL]:https://msdn.microsoft.com/library/ms143726.aspx
[Índices não clusterizados em índices columnstore clusterizados]:https://msdn.microsoft.com/library/ms188783.aspx
[Varchar (max)]:https://msdn.microsoft.com/library/ms176089.aspx
[nvarchar (max)]:https://msdn.microsoft.com/library/ms186939.aspx
[varbinary (max)]:https://msdn.microsoft.com/library/ms188362.aspx
[SYSNAME]:https://msdn.microsoft.com/library/ms188021.aspx
[SELECIONE... EM]:https://msdn.microsoft.com/library/ms188029.aspx
[sp_spaceused()]:https://msdn.microsoft.com/library/ms188776.aspx
[Tabelas largas]:https://msdn.microsoft.com/library/ms143432.aspx
[BULK INSERT]:https://msdn.microsoft.com/library/ms188365.aspx
[utilitário bcp]:https://msdn.microsoft.com/library/ms162802.aspx
[UNIQUEIDENTIFIER]:https://msdn.microsoft.com/library/ms187942.aspx
[NUMÉRICO]:https://msdn.microsoft.com/library/ms187746.aspx
[ROWS ou RANGE]:https://msdn.microsoft.com/library/ms189461.aspx
[FIRST_VALUE]:https://msdn.microsoft.com/library/hh213018.aspx
[LAST_VALUE]:https://msdn.microsoft.com/library/hh231517.aspx
[CUME_DIST]:https://msdn.microsoft.com//library/hh231078.aspx
[PERCENT_RANK]:https://msdn.microsoft.com/library/hh213573.aspx
[CHECKSUM()]:https://msdn.microsoft.com/library/ms189788.aspx
[BINARY_CHECKSUM()]:https://msdn.microsoft.com/library/ms173784.aspx
[HAS_PERMS_BY_NAME()]:https://msdn.microsoft.com/library/ms189802.aspx
[NEWID)]:https://msdn.microsoft.com/library/ms190348.aspx
[RAND)]:https://msdn.microsoft.com/library/ms177610.aspx


  

  


