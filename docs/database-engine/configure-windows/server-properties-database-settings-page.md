---
title: "Propriedades do Servidor (p&#225;gina Configura&#231;&#245;es de Banco de Dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.serverproperties.databasesettings.f1"
ms.assetid: 1cebdbd3-cbfd-4a02-bba6-a5addf4e3ada
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# Propriedades do Servidor (p&#225;gina Configura&#231;&#245;es de Banco de Dados)
  Use esta página para exibir ou modificar suas configurações de banco de dados.  
  
## Opções  
 **Fator de preenchimento padrão do índice**  
 Especifica o quanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve preencher cada página ao criar um índice novo usando dados existentes. O fator de preenchimento afeta o desempenho porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa de tempo para dividir páginas quando elas está cheias.  
  
 O valor padrão é 0; os valores válidos variam de 0 a 100. Um fator de preenchimento de 0 ou 100 cria índices clusterizados com páginas inteiras de dados e índices não clusterizados com páginas inteiras de folhas, mas deixa algum espaço no nível superior da árvore de índice. Os valores 0 e 100 do fator de preenchimento são idênticos em todos os aspectos.  
  
 Os valores pequenos do fator de preenchimento levam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para criar índices com páginas que não estão cheias. Cada índice ocupa mais espaço de armazenamento, mas há mais espaço para inserções subsequentes sem exigência de divisões de página.  
  
 **Esperar indefinidamente**  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não terá limite de tempo ao esperar uma nova fita de backup.  
  
 **Tentar uma vez**  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] terá limite de tempo se uma fita de backup não estiver disponível quando necessário.  
  
 **Tentar durante minuto(s)**  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] terá limite de tempo se uma fita de backup não estiver disponível dentro do tempo especificado.  
  
 **Retenção de mídia de backup padrão (em dias)**  
 Fornece um padrão de função de sistema durante a retenção de cada meio de backup depois que ele tenha sido usado para um backup de banco de dados ou backup de log de transações. Essa opção ajuda a proteger os backups para que não sejam substituídos até que o número especificado de dias tenha se passado.  
  
 **Compactar backup**  
 No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou versões posteriores), indica a configuração atual da opção **padrão de compactação de backup**. Essa opção determina o padrão do nível de servidor para backups compactados, como segue:  
  
-   Se a caixa **Compactar backup** estiver em branco, novos backups são descompactados por padrão.  
  
-   Se a caixa **Compactar backup** estiver marcada, novos backups serão compactados por padrão.  
  
    > [!IMPORTANT]  
    >  Por padrão, a compactação aumenta consideravelmente o uso da CPU, e o consumo adicional da CPU por parte do processo de compactação pode afetar negativamente as operações simultâneas. Portanto, é recomendável criar backups compactados de baixa prioridade em uma sessão cujo uso da CPU é limitado pelo [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md). Para obter mais informações, consulte [Usar o Administrador de Recursos para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).  
  
 Se você for membro da função de servidor fixa **sysadmin** ou **serveradmin** , será possível alterar a configuração clicando na caixa **Compactar backup** .  
  
 Para obter mais informações, consulte [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) e [Compactação de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
 **Intervalo de recuperação (minutos)**  
 Define o número máximo de minutos por banco de dados para a recuperação de bancos de dados. O padrão é 0, que indica configuração automática pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Na prática, isso significa um tempo de recuperação inferior a um minuto e um ponto de verificação a cada um minuto aproximadamente para bancos de dados ativos. Para obter mais informações, consulte [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md).  
  
 **Dados**  
 Especifica o local padrão para arquivos de dados. Clique no botão Procurar para navegar para um novo local padrão. As alterações não entrarão em vigor até que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja reinicializado.  
  
 **Log**  
 Especifica o local padrão para arquivos de log. Clique no botão Procurar para navegar para um novo local padrão. As alterações não entrarão em vigor até que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja reinicializado.  
  
 **Valores Configurados**  
 Exibe os valores configurados para as opções nesse painel. Se você alterar esses valores, clique em **Executando Valores** para verificar se as alterações entraram em vigor. Se não tiverem, a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser redeclarada primeiro.  
  
 **Executando Valores**  
 Exiba os valores que estão sendo executados para as opções neste painel. Esses valores são somente leitura.  
  
## Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
  