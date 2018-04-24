---
title: Configurar a inicialização instantânea de arquivo - Analytics Platform System | Microsoft Docs
description: Configure a inicialização instantânea de arquivo no sistema de plataforma de análise. A inicialização instantânea de arquivo é um recurso do SQL Server que permite operações de arquivo de dados ser executado mais rapidamente.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 20498cc4e2c4ad959fce263984b58e3186630cea
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="instant-file-initialization-configuration"></a>Configuração de inicialização instantânea de arquivo
A inicialização instantânea de arquivo é um recurso do SQL Server que permite operações de arquivo de dados ser executado mais rapidamente. Marcando a caixa para ativar a inicialização instantânea de arquivo melhorará o desempenho do SQL Server PDW. No entanto, se isso representa um risco de segurança para você business, em seguida, deixe a caixa desmarcada.  
  
> [!IMPORTANT]  
> Quando a inicialização instantânea de arquivo é habilitada, do SQL Server não substituirá bits excluídos com zeros.  Esse comportamento pode criar uma vulnerabilidade de segurança se usuários não autorizados acessem os dados excluídos. No entanto, o SQL Server PDW reduz esse risco, garantindo que o banco de dados do SQL Server e os arquivos de backup são sempre anexados a uma instância do SQL Server. a conta de serviço do SQL Server e o administrador local podem acessar os dados excluídos no SQL Server PDW.  
  
A inicialização instantânea de arquivo não está disponível quando a TDE está habilitada.  
  
## <a name="add-permission-for-the-backup-account"></a>Adicionar a permissão para a conta de Backup  
O processo de backup requer uma credencial de rede (conta de usuário do Windows) que pode acessar o local de armazenamento de backup. Autorizar o PDW para usar a conta usando o [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimento. Consulte [BACKUP de banco de dados](../t-sql/statements/backup-database-parallel-data-warehouse.md) por todo o processo de backup. Para usar a inicialização instantânea de arquivo, a conta de backup deve ser concedida a `Perform volume maintenance tasks` permissão.  
  
1.  No servidor de backup, abra o **política de segurança Local** aplicativo (`secpol.msc`).  
  
2.  No painel esquerdo, expanda **Políticas Locais**e, em seguida, clique em **Atribuição de Direitos de Usuário**.  
  
3.  No painel direito, clique duas vezes em **Executar tarefas de manutenção de volume**.  
  
4.  Clique em **Adicionar Usuário ou Grupo** e adicione as contas de usuário que são usadas ​​para backups.  
  
5.  Clique em **Aplicar**e feche todas as caixas de diálogo **Política de Segurança Local** .  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>Para ativar ou desativar a inicialização instantânea de arquivo  
  
1.  Inicie o Gerenciador de configuração. Para obter mais informações, consulte [iniciar o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do Gerenciador de configuração, clique em **inicialização imediata de arquivo**.  
  
3.  Para ativar a inicialização instantânea de arquivo, marque a caixa ao lado de **habilitar a inicialização imediata de arquivo em todos os nós**. Para desativar a inicialização instantânea de arquivo, desmarque a caixa ao lado de **habilitar a inicialização imediata de arquivo em todos os nós**.  
  
    > [!WARNING]  
    > Quando você desativa a inicialização instantânea de arquivo, a consideração de segurança discutida acima para o recurso pode ainda se aplicam a arquivos excluídos durante a inicialização instantânea de arquivo foi habilitada.  
  
4.  Clique em **Aplicar**. As alterações serão propagadas por meio de instâncias do SQL Server no SQL Server PDW na próxima vez em que os serviços de aplicativo são reiniciados. Para reiniciar os serviços do dispositivo, consulte [Status de serviços PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).  
  
5.  Talvez você queira repetir os passos descritos acima como **adicionar permissão para a conta de Backup** para remover o **executar tarefas de manutenção de volume** permissão.  
  
![Dispositivo DWConfig PDW inicialização de arquivo instantânea](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
Para obter mais informações sobre a inicialização instantânea de arquivo, consulte [inicialização imediata de arquivo](http://technet.microsoft.com/en-us/library/ms175935(v=SQL.105).aspx).  
  
