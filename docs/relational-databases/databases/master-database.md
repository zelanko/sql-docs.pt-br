---
title: Banco de dados mestre | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], about
- master database [SQL Server]
ms.assetid: 660e909f-61eb-406b-bbce-8864dd629ba0
caps.latest.revision: 50
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7d33bb332481561a1a81c0d18ebcfb19b4fc32f7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32930981"
---
# <a name="master-database"></a>Banco de dados mestre
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O banco de dados **master** registra todas as informações no nível de sistema para um sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isto inclui metadados de ampla instância como contas de logon, pontos de extremidade, servidores vinculados e parâmetros de configuração de sistema. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os objetos de sistema não são mais armazenados no banco de dados **mestre** ; em vez disso, eles são armazenados no [Banco de dados de recurso](../../relational-databases/databases/resource-database.md). Além disso, **mestre** é o banco de dados que registra a existência de todos os outros bancos de dados e o local desses arquivos de bancos de dados, e registra as informações de inicialização para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá iniciar se o banco de dados **mestre** não estiver disponível.  
  
## <a name="physical-properties-of-master"></a>Propriedades físicas de mestre  
 A tabela a seguir lista os valores iniciais de configuração dos dados **mestre** e dos arquivos de log. Os tamanhos desses arquivos podem variar um pouco em diferentes edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Arquivo|Nome lógico|Nome físico|Aumento do arquivo|  
|----------|------------------|-------------------|-----------------|  
|Dados primários|master|master.mdf|Aumento automático de 10 por cento até que o disco fique cheio.|  
|Log|mastlog|mastlog.ldf|Aumento automático de 10 por cento para um máximo de 2 terabytes.|  
  
 Para obter informações sobre como mover os dados **master** e os arquivos de log, veja [Mover bancos de dados do sistema](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options"></a>Opções de banco de dados  
 A tabela a seguir lista o valor padrão de cada opção de banco de dados no banco de dados **mestre** e se a opção pode ser modificada. Para exibir as configurações atuais dessas opções, use a exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Opção de banco de dados|Valor padrão|Pode ser modificado|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|não|  
|ANSI_NULL_DEFAULT|OFF|Sim|  
|ANSI_NULLS|OFF|Sim|  
|ANSI_PADDING|OFF|Sim|  
|ANSI_WARNINGS|OFF|Sim|  
|ARITHABORT|OFF|Sim|  
|AUTO_CLOSE|OFF|não|  
|AUTO_CREATE_STATISTICS|ON|Sim|  
|AUTO_SHRINK|OFF|não|  
|AUTO_UPDATE_STATISTICS|ON|Sim|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sim|  
|CHANGE_TRACKING|OFF|não|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sim|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sim|  
|CURSOR_DEFAULT|GLOBAL|Sim|  
|Opções de disponibilidade de banco de dados|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|não<br /><br /> não<br /><br /> não|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sim|  
|DB_CHAINING|ON|não|  
|ENCRYPTION|OFF|não|  
|MIXED_PAGE_ALLOCATION|ON|não|  
|NUMERIC_ROUNDABORT|OFF|Sim|  
|PAGE_VERIFY|CHECKSUM|Sim|  
|PARAMETERIZATION|SIMPLE|Sim|  
|QUOTED_IDENTIFIER|OFF|Sim|  
|READ_COMMITTED_SNAPSHOT|OFF|não|  
|RECOVERY|SIMPLE|Sim|  
|RECURSIVE_TRIGGERS|OFF|Sim|  
|Opções do Service Broker|DISABLE_BROKER|não|  
|TRUSTWORTHY|OFF|Sim|  
  
 Para obter uma descrição dessas opções de banco de dados, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="restrictions"></a>Restrictions  
 As seguintes operações não podem ser executadas no banco de dados **mestre** :  
  
-   Adicionando arquivos ou grupos de arquivos.  
  
-   Alteração de agrupamento. O agrupamento padrão é o agrupamento de servidor.  
  
-   Alteração do proprietário do banco de dados. **master** pertence a **sa**.  
  
-   Criando um catálogo de texto completo ou índice de texto completo.  
  
-   Criando gatilhos em tabelas do sistema no banco de dados.  
  
-   Descartando o banco de dados.  
  
-   Descartando o usuário **convidado** do banco de dados.  
  
-   Habilitação do Change Data Capture.  
  
-   Participação no espelhamento de banco de dados.  
  
-   Remoção do grupo de arquivos primário, arquivo de dados primário ou arquivo de log.  
  
-   Renomeação do banco de dados ou grupo de arquivos primário.  
  
-   Definindo o banco de dados como OFFLINE.  
  
-   Definindo o banco de dados ou grupo de arquivos primário como READ_ONLY.  
  
## <a name="recommendations"></a>Recomendações  
 Ao trabalhar com o banco de dados **mestre** , considere as seguintes recomendações:  
  
-   Sempre tenha um backup atual do banco de dados **mestre** disponível.  
  
-   Faça backup do banco de dados **mestre** o mais cedo possível depois das seguintes operações:  
  
    -   Criando, modificando ou descartando qualquer banco de dados  
  
    -   Alterando servidor ou valores de configuração de banco de dados  
  
    -   Modificando ou adicionando contas de logon  
  
-   Não crie objetos de usuário no **mestre**. Se você fizer isso, será necessário fazer backup do **mestre** com mais frequência.  
  
-   Não defina a opção TRUSTWORTHY como ON para o banco de dados **mestre** .  
  
## <a name="what-to-do-if-master-becomes-unusable"></a>O que fazer se o mestre ficar inutilizável  
 Se o **mestre** se tornar inutilizável, você poderá retornar o banco de dados a um estado utilizável das seguintes maneiras:  
  
-   Restaure o **mestre** a partir de um backup de banco de dados atual.  
  
     Se você puder iniciar a instância de servidor, deverá poder restaurar o **mestre** a partir de um backup de banco de dados completo. Para obter mais informações, veja [Restaurar o banco de dados mestre &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md).  
  
-   Recrie completamente o **mestre** .  
  
     Se danos graves do **master** impedirem a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], recrie o **master**. Para obter mais informações, consulte [Recriar bancos de dados do sistema](../../relational-databases/databases/rebuild-system-databases.md).  
  
    > [!IMPORTANT]  
    >  A recriação de **master** recria todos os bancos de dados do sistema.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Recriar bancos de dados do sistema](../../relational-databases/databases/rebuild-system-databases.md)  
  
 [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
 [Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)  
  
  
