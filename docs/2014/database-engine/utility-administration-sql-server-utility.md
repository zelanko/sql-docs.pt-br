---
title: Administração do utilitário (Utilitário do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 3e5a00c3-8905-40f0-9ddc-d924df9c2f0d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fca4ea655ffdcf8471d1340016d16f2c5b9c352a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927661"
---
# <a name="utility-administration-sql-server-utility"></a>Administração do Utilitário (Utilitário do SQL Server)
  Use as guias de Administração do Utilitário para gerenciar configurações de políticas, segurança e data warehouse para um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Utility. Para obter mais informações sobre os conceitos do Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , veja [Recursos e tarefas do Utilitário do SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 Guia Política - Use a guia Política para exibir ou especificar políticas de monitoramento globais.  
  
 Definir políticas de monitoramento de aplicativo da camada de dados. Para expandir a lista de valores dessa opção, clique na seta ao lado do nome da política ou clique no título da política.  
 Quando um aplicativo está executando com capacidade insuficiente do processador? Para alterar essa política, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do processador é 70%.  
  
-   O valor padrão mínimo para utilização do processador é 0%.  
  
 Quando um aplicativo está executando com espaço de arquivo insuficiente? Para alterar a política de utilização de espaço de arquivos de dados ou de log, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do espaço de arquivo é 70%.  
  
-   O valor padrão mínimo para utilização do espaço de arquivo é 0%.  
  
 Definir políticas globais de monitoramento de aplicativo de instância gerenciada do SQL Server. Para expandir a lista de valores dessa opção, clique na seta ao lado do nome da política ou clique no título da política.  
 Quando uma instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está executando com capacidade insuficiente de processador? Para alterar essa política, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do processador de instância é 70%.  
  
-   O valor padrão mínimo para utilização do processador de instância é 0%.  
  
 Quando uma instância gerenciada do computador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está executando com capacidade insuficiente de processador? Para alterar essa política, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do processador do computador é 70%.  
  
-   O valor padrão mínimo para utilização do processador do computador é 0%.  
  
 Quando uma instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está executando com espaço de arquivo insuficiente? Para alterar a política de utilização de espaço de arquivos de dados ou de log, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do espaço de arquivo é 70%.  
  
-   O valor padrão mínimo para utilização do espaço de arquivo é 0%.  
  
 Quando uma instância gerenciada do computador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está executando com volume de armazenamento insuficiente? Para alterar essa política, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do espaço do volume do computador é 70%.  
  
-   O valor padrão mínimo para utilização do espaço do volume do computador é 0%.  
  
 Reduzindo o ruído de violação de políticas em recursos altamente voláteis. Para expandir os controles desse recurso, clique na seta para baixo à direita da exibição.  
 Para obter mais informações, veja [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 Guia Segurança - Exibe nomes de logon com permissões de administração ou leitura no UCP.  
  
 Selecione os logons do UCP que serão adicionados à função Leitor do Utilitário.  
 O privilégio de Leitor do Utilitário permite que a conta de usuário:  
  
-   Conecte-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Utility.  
  
-   Veja todos os pontos de vista no Gerenciador do Utilitário no SSMS.  
  
-   Consulte configurações no nó Administração do Utilitário no Gerenciador do Utilitário no SSMS.  
  
 Os administradores do utilitário podem inscrever instâncias do SQL Server no Utilitário do SQL Server e removê-las, bem como modificar políticas em instâncias gerenciadas e modificar configurações de administração no UCP.  
  
 Para ser um administrador do Utilitário, você deve ter privilégios de sysadmin na instância do SQL Server. Para adicionar ou alterar contas de usuário para o UCP do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use Pesquisador de Objetos no SSMS para adicionar o usuário aos logons do servidor da instância do UCP do SQL Server. Para obter mais informações, veja [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql).  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 Guia Data Warehouse - Exibe os detalhes da configuração do data warehouse de gerenciamento do utilitário.  
  
 Retenção de dados  
 Especifique o período de retenção de dados de informações de utilização coletadas para instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O período padrão é de 1 ano. O valor mínimo é 1 mês. O valor com suporte mais longo é 2 anos.  
  
 Informações de Configuração do Data Warehouse do Utilitário  
 Os parâmetros de configuração a seguir não podem ser configurados nesta versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Nome do UMDW: Sysutility_mdw_ \<GUID> _DATA.  
  
-   Frequência de carregamento do conjunto de coleta: a cada 15 minutos.  
  
 O diretório UMDW é configurável: \<System drive> : \Program Files\Microsoft SQL Server \ MSSQL10_50. <UCP_Name> \MSSQL\Data \\ , onde \<System drive> é normalmente o C:\ Dirigir. O arquivo de log, UMDW_ \<GUID> _LOG, está localizado no mesmo diretório.  
  
> [!NOTE]  
>  O local do arquivo UMDW (sysutility_mdw) pode ser alterado usando-se desanexar/anexar ou ALTER DATABASE. É recomendável usar ALTER DATABASE. Para obter mais informações, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
 Voltar aos padrões prontos para uso  
 Para redefinir as configurações nessa guia para os valores padrão, clique no botão **Restaurar Padrões** e em **Aplicar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Painel do utilitário &#40;Utilitário do SQL Server&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [Detalhes do aplicativo da camada de dados implantados &#40;Utilitário do SQL Server&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [Detalhes do Instância Gerenciada &#40;Utilitário do SQL Server&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [Monitorar instâncias do SQL Server no Utilitário do SQL Server](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
  
