---
title: Fazer upgrade do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4767b695f0c2c3668278e30f47f389664b4a4ef0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189546"
---
# <a name="upgrade-database-engine"></a>Atualizar o Mecanismo de Banco de Dados
  Este tópico fornece as informações necessárias para preparar e entender o processo de atualização; ele abrange:  
  
-   Problemas de atualização conhecidos.  
  
-   Tarefas e considerações da pré-atualização.  
  
-   Links para tópicos de procedimento para a atualização do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Links para tópicos de procedimento para a migração de bancos de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Considerações sobre agrupamentos de failover.  
  
-   Tarefas posteriores à atualização e considerações.  
  
## <a name="known-upgrade-issues"></a>Problemas de atualização conhecidos  
 Antes de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], analise o tópico [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../sql-server-database-engine-backward-compatibility.md). Para obter mais informações sobre cenários de atualização compatíveis e problemas conhecidos de atualização, consulte [Versões com Suporte e Atualizações de Edição](supported-version-and-edition-upgrades.md). Para obter conteúdo de compatibilidade com versões anteriores para outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Compatibilidade com Versões Anteriores](../../getting-started/backward-compatibility.md).  
  
> [!IMPORTANT]  
>  Antes de atualizar de uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra, verifique se há suporte à funcionalidade usada atualmente na edição para a qual está atualizando.  
  
> [!NOTE]  
>  Quando você atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de uma versão anterior da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise, escolha entre Enterprise Edition: Licenciamento baseado em núcleo e Enterprise Edition. Estas edições Enterprise só diferem com relação aos modos de licenciamento. Para saber mais, confira [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
## <a name="pre-upgrade-checklist"></a>Lista de verificação anterior à atualização  
 O programa de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de uma versão anterior. Também é possível migrar bancos de dados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A migração pode ser feita de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra no mesmo computador ou de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em outro computador. Opções de migração incluem o uso do Assistente para cópia de banco de dados, Backup e restauração a funcionalidade, uso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] métodos de importação exportação em massa/em massa e Assistente para exportação e importação.  
  
 Antes de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], revise o seguinte:  
  
-   Analise os [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Analise os [Check Parameters for the System Configuration Checker](check-parameters-for-the-system-configuration-checker.md).  
  
-   Analise os [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
-   Examine o tópico [Atualizações de versão e edição com suporte](supported-version-and-edition-upgrades.md).  
  
-   Analise o tópico [Usar o Supervisor de Atualização para preparar para atualizações](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
-   Analise o tópico [Usar o Distributed Replay Utility para preparar para atualizações](../../sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md).  
  
-   Analise o tópico [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../sql-server-database-engine-backward-compatibility.md).  
  
-   Analise o tópico [Migrar planos de consulta](change-the-database-compatibility-mode-and-use-the-query-store.md).  
  
 Examine os seguintes problemas e faça alterações antes de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Ao atualizar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é inscrito em relações de MSX/TSX, atualize os servidores de destino antes de atualizar os servidores mestres. Se você atualizar servidores mestres antes de servidores de destino, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não poderá se conectar a instâncias principais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Ao atualizar de uma edição de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma edição de 64 bits do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é necessário atualizar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] antes de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Faça backup de todos os arquivos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da instância a ser atualizada, para que seja possível restaurá-los se isso for necessário.  
  
-   Execute os comandos DBCC (Database Console Commands) apropriados nos bancos de dados a serem atualizados para verificar se eles se encontram em um estado consistente.  
  
-   Calcule o espaço em disco necessário para atualizar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , além dos bancos de dados de usuários. Para obter o espaço em disco necessário pelos componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Requisitos de Hardware e Software para Instalar o SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Verifique se os bancos de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existentes - master, model, msdb e tempdb - estão configurados para crescimento automático e verifique se eles têm espaço suficiente no disco rígido.  
  
-   Verifique se todos os servidores de banco de dados têm informações de logon no banco de dados mestre. Isso é importante para restaurar um banco de dados, pois as informações de logon de sistema residem em master.  
  
-   Desabilite todos os procedimentos armazenados de inicialização, pois o processo de atualização irá interromper e iniciar serviços na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo atualizada. Os procedimentos armazenados processados no momento da inicialização podem bloquear o processo de atualização.  
  
-   Certifique-se que a Replicação esteja atualizada e interrompa-a.  
  
-   Encerre todos os aplicativos, inclusive todos os serviços que dependam do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A atualização poderá falhar se aplicativos locais forem conectados à instância que está sendo atualizada.  
  
-   Se você usa Espelhamento de Banco de Dados, consulte [Minimizar o tempo de inatividade para bancos de dados espelhados ao atualizar instâncias do servidor](../database-mirroring/upgrading-mirrored-instances.md).  
  
## <a name="upgrading-the-database-engine"></a>Atualizando o Mecanismo de Banco de Dados  
 Você pode substituir uma instalação do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior por uma atualização de versão. Se uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for detectada ao executar a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , todos os arquivos de programas anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão atualizados e todos os dados armazenados na instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão preservados. Além disso, as versões anteriores dos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerão intactas no computador.  
  
> [!WARNING]  
>  Ao executar o programa de instalação do SQL Server 2014, a instância do SQL Server é interrompida e reiniciada como parte da execução das verificações pré-atualização.  
  
> [!CAUTION]  
>  Quando você atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será substituída e não mais existirá no computador. Antes de atualizar, faça backup dos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de outros objetos associados à instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Você pode atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] por meio do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="database-compatibility-level-after-upgrade"></a>Nível de compatibilidade do banco de dados após a atualização  
 Os níveis de compatibilidade do `tempdb`, `model`, `msdb` e **recurso** bancos de dados são definidos como 120 depois da atualização. O banco de dados do sistema `master` mantém o nível de compatibilidade anterior à atualização.  
  
 Se o nível de compatibilidade de um banco de dados de usuário era 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade era 90 antes da atualização, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Novos bancos de dados do usuário herdará o nível de compatibilidade de `model` banco de dados.  
  
## <a name="migrating-databases"></a>Migrando bancos de dados  
 É possível mover bancos de dados do usuário para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio das funcionalidades de backup e restauração ou anexação e desanexação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Copiar bancos de dads com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md) ou [Desanexar e anexar banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
> [!IMPORTANT]  
>  Um banco de dados que tenha o nome idêntico em servidores de origem e de destino não pode ser movido ou copiado. Nesse caso, ele será anotado como "Já existe".  
  
 Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="after-upgrading-the-database-engine"></a>Depois de atualizar o Mecanismo de Banco de Dados  
 Depois de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], conclua as seguintes tarefas:  
  
-   Registre novamente seus servidores. Para obter mais informações sobre como registrar servidores, consulte [Registrar Servidores](../../ssms/register-servers/register-servers.md).  
  
-   Preencha novamente catálogos de texto completo para garantir a consistência semântica em resultados da consulta.  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instala novos separadores de palavras para uso pela Pesquisa semântica e de texto completo. Os separadores de palavras são usados na indexação e na consulta. Se você não recriar os catálogos de texto completo, seus resultados da pesquisa poderão ser inconsistentes. Se você emitir uma consulta de texto completo que procura uma frase que é interrompida diferentemente pelo separador de palavras em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o separador de palavras atual, um documento ou linha contendo a frase talvez não seja recuperada. Isso ocorre porque as frases indexadas foram quebradas usando uma lógica diferente da usada pela consulta. A solução é preencher novamente (recompilar) os catálogos de texto completo com os novos separadores de palavras de forma que os comportamentos de tempo de indexação e de consulta sejam idênticos.  
  
     Para obter mais informações, consulte [sp_fulltext_catalog &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql).  
  
-   Configure a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para reduzir a área da superfície de um sistema vulnerável a ataques, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala e habilita seletivamente serviços e recursos essenciais.  
  
-   Valide ou remova as dicas de USE PLAN geradas pelo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e aplicadas a consultas em tabelas e índices particionados.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Altera a maneira de consultas em tabelas e índices particionados são processadas. As consultas em objetos particionados que usam a dica USE PLAN para um plano gerado pelo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] podem conter um plano que não pode ser usado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Recomenda-se os seguintes procedimentos após a atualização do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
     **Quando a dica USE PLAN é especificada diretamente em uma consulta:**  
  
    1.  Remova a dica USE PLAN da consulta.  
  
    2.  Teste a consulta.  
  
    3.  Se o otimizador não selecionar um plano apropriado, ajuste a consulta e considere a especificação da dica USE PLAN com o plano de consulta desejado.  
  
     **Quando a dica USE PLAN é especificada em um guia de plano:**  
  
    1.  Use a função sys.fn_validate_plan_guide para verificar a validade da guia de plano. Como alternativa, é possível verificar se existem planos inválidos por meio do evento Guia de Plano sem Êxito no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
    2.  Se a guia de plano não for válida, descarte-a. Se o otimizador não selecionar um plano apropriado, ajuste a consulta e considere a especificação da dica USE PLAN com o plano de consulta desejado.  
  
     Um plano inválido não causará a falha da consulta quando a dica USE PLAN for especificada em uma guia de plano. Em vez disso, a consulta será compilada sem usar a dica USE PLAN.  
  
 Quaisquer bancos de dados que foram marcados como habilitados ou desabilitados para texto completo antes da atualização manterão esse status depois de atualização. Depois da atualização, os catálogos de texto completo serão reconstruídos e populados automaticamente para todos os bancos de dados habilitados para texto completo. Essa é uma operação demorada e que consume recursos. Você pode pausar temporariamente a operação de indexação de texto completo executando a seguinte instrução:  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 1;  
```  
  
 Para retomar a população do índice de texto completo, execute a seguinte instrução:  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 0;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Atualizações de versão e edição com suporte](supported-version-and-edition-upgrades.md)   
 [Trabalhar com várias versões e instâncias do SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [Compatibilidade com versões anteriores](../../getting-started/backward-compatibility.md)   
 [Atualizar bancos de dados replicados](upgrade-replicated-databases.md)  
  
  
