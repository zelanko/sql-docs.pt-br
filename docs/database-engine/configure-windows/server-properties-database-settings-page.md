---
title: Propriedades do servidor (página Configurações do Banco de Dados) | Microsoft Docs
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.databasesettings.f1
ms.assetid: 1cebdbd3-cbfd-4a02-bba6-a5addf4e3ada
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.custom: ''
ms.date: 05/23/2019
ms.openlocfilehash: bf30a65cf0390c5b8400fe7a390520e4bdb29994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66771764"
---
# <a name="server-properties---database-settings-page"></a>Propriedades do servidor – página Configurações do Banco de Dados

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta página para exibir ou modificar suas configurações de banco de dados.  
  
## <a name="options"></a>Opções

### <a name="default-index-fill-factor"></a>Fator de preenchimento padrão do índice

Especifica o quanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve preencher cada página ao criar um índice novo usando dados existentes. O fator de preenchimento afeta o desempenho porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa de tempo para dividir páginas quando elas está cheias.
  
O valor padrão é 0; os valores válidos variam de 0 a 100. Um fator de preenchimento de 0 ou 100 cria índices clusterizados com páginas inteiras de dados e índices não clusterizados com páginas inteiras de folhas, mas deixa algum espaço no nível superior da árvore de índice. Os valores 0 e 100 do fator de preenchimento são idênticos em todos os aspectos.
  
Os valores pequenos do fator de preenchimento levam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para criar índices com páginas que não estão cheias. Cada índice ocupa mais espaço de armazenamento, mas há mais espaço para inserções subsequentes sem exigência de divisões de página.
  
### <a name="wait-indefinitely"></a>Esperar indefinidamente

Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não terá limite de tempo ao esperar uma nova fita de backup.  

### <a name="try-once"></a>Tentar uma vez

Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] terá limite de tempo se uma fita de backup não estiver disponível quando necessário.

### <a name="try-for-minutes"></a>Tentar durante minuto(s)

Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] terá limite de tempo se uma fita de backup não estiver disponível dentro do tempo especificado.  

### <a name="default-backup-media-retention-in-days"></a>Retenção de mídia de backup padrão (em dias)

Fornece um padrão de função de sistema durante a retenção de cada meio de backup depois que ele tenha sido usado para um backup de banco de dados ou backup de log de transações. Essa opção ajuda a proteger os backups para que não sejam substituídos até que o número especificado de dias tenha se passado.  

#### <a name="compress-backup"></a>Compactar backup

No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou versões posteriores), indica a configuração atual da opção **padrão de compactação de backup** . Essa opção determina o padrão do nível de servidor para backups compactados, como segue:

- Se a caixa **Compactar backup** estiver em branco, novos backups são descompactados por padrão.

- Se a caixa **Compactar backup** estiver marcada, novos backups serão compactados por padrão.
  
    > [!IMPORTANT]
    >  Por padrão, a compactação aumenta consideravelmente o uso da CPU, e o consumo adicional da CPU por parte do processo de compactação pode afetar negativamente as operações simultâneas. Portanto, é recomendável criar backups compactados de baixa prioridade em uma sessão cujo uso da CPU é limitado pelo [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md). Para obter mais informações, consulte [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../.. relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).
  
Se você for membro da função de servidor fixa **sysadmin** ou **serveradmin** , será possível alterar a configuração clicando na caixa **Compactar backup** .  
  
Para obter mais informações, consulte [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) e [Compactação de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).  

#### <a name="backup-checksum"></a>Soma de verificação de backup

Essa opção permite ativar/desativar a configuração sp_configure para o *padrão de soma de verificação de backup*. Esse recurso facilita a habilitação do padrão de soma de verificação de backup.

### <a name="recovery-interval-minutes"></a>Intervalo de recuperação (minutos)

Define o número máximo de minutos por banco de dados para a recuperação de bancos de dados. O padrão é 0, que indica configuração automática pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Na prática, essa opção significa um tempo de recuperação inferior a um minuto e um ponto de verificação com um intervalo de aproximadamente um minuto para bancos de dados ativos. Para obter mais informações, consulte [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md).  
  
### <a name="data"></a>data

Especifica o local padrão para arquivos de dados. Clique no botão Procurar para navegar para um novo local padrão. As alterações não entram em vigor enquanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é reinicializado.  
  
### <a name="log"></a>Log
  
Especifica o local padrão para arquivos de log. Clique no botão Procurar para navegar para um novo local padrão. As alterações não entram em vigor enquanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é reinicializado.  
  
### <a name="configured-values"></a>Valores configurados

Exibe os valores configurados para as opções nesse painel. Se você alterar esses valores, clique em **Executando Valores** para verificar se as alterações entraram em vigor. Caso contrário, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisará primeiro ser declarada novamente.  
  
### <a name="running-values"></a>Como executar valores

Exiba os valores que estão sendo executados para as opções neste painel. Esses valores são somente leitura.  
  
## <a name="see-also"></a>Consulte Também

- [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

- [Especificar o fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)