---
title: Configurar a inicialização instantânea de arquivo - Analytics Platform System | Microsoft Docs
description: Configure a inicialização instantânea de arquivo no Analytics Platform System. Inicialização instantânea de arquivo é um recurso do SQL Server que permite que operações de arquivo de dados ser executado mais rapidamente.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 959d219565de6577e31d9548f5daea0fe0d2419e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298133"
---
# <a name="instant-file-initialization-configuration"></a>Configuração da inicialização instantânea de arquivo
Inicialização instantânea de arquivo é um recurso do SQL Server que permite que operações de arquivo de dados ser executado mais rapidamente. Marcando a caixa para ativar a inicialização instantânea de arquivo melhorará o desempenho do SQL Server PDW. No entanto, se isso representa um risco de segurança para você business, em seguida, deixe a caixa desmarcada.  
  
> [!IMPORTANT]  
> Quando a inicialização instantânea de arquivo está habilitada, SQL Server não substituirá bits excluídos com zeros.  Esse comportamento foi possível criar uma vulnerabilidade de segurança se usuários não autorizados obtiverem acesso aos dados excluídos. No entanto, o SQL Server PDW diminui esse risco, garantindo que o banco de dados do SQL Server e os arquivos de backup são sempre anexados a uma instância do SQL Server; a conta de serviço do SQL Server e o administrador local podem acessar os dados excluídos no SQL Server PDW.  
  
A inicialização instantânea de arquivo não está disponível quando a TDE está habilitada.  
  
## <a name="add-permission-for-the-backup-account"></a>Adicionar a permissão para a conta de Backup  
O processo de backup requer uma credencial de rede (conta de usuário do Windows) que pode acessar o local de armazenamento de backup. Autorizar o PDW para usar a conta usando o [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimento. Ver [BACKUP do banco de dados](../t-sql/statements/backup-database-parallel-data-warehouse.md) para todo o processo de backup. Para usar a inicialização instantânea de arquivo, a conta de backup deve ser concedida a `Perform volume maintenance tasks` permissão.  
  
1.  No servidor de backup, abra o **política de segurança Local** aplicativo (`secpol.msc`).  
  
2.  No painel esquerdo, expanda **Políticas Locais**e, em seguida, clique em **Atribuição de Direitos de Usuário**.  
  
3.  No painel direito, clique duas vezes em **Executar tarefas de manutenção de volume**.  
  
4.  Clique em **Adicionar Usuário ou Grupo** e adicione as contas de usuário que são usadas ​​para backups.  
  
5.  Clique em **Aplicar**e feche todas as caixas de diálogo **Política de Segurança Local** .  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>Para ativar ou desativar a inicialização instantânea de arquivo  
  
1.  Inicie o Gerenciador de configuração. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do Gerenciador de configuração, clique em **inicialização instantânea de arquivo**.  
  
3.  Para ativar a inicialização instantânea de arquivo, marque a caixa ao lado **habilitar a inicialização instantânea de arquivo em todos os nós**. Para desativar a inicialização instantânea de arquivo, desmarque a caixa ao lado **habilitar a inicialização instantânea de arquivo em todos os nós**.  
  
    > [!WARNING]  
    > Quando você desativar a inicialização instantânea de arquivo, a consideração de segurança discutida acima para o recurso pode ainda se aplicam a arquivos excluídos enquanto a inicialização instantânea de arquivo estava habilitada.  
  
4.  Clique em **Aplicar**. As alterações serão propagadas por meio de instâncias do SQL Server no SQL Server PDW na próxima vez em que os serviços de dispositivo são reiniciados. Para reiniciar os serviços do dispositivo, consulte [Status de serviços do PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).  
  
5.  Talvez você queira repetir os passos descritos acima, como **adicionar a permissão para a conta de Backup** para remover o **executar tarefas de manutenção de volume** permissão.  
  
![DWConfig Appliance PDW Instant File Initialization](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
Para obter mais informações sobre a inicialização instantânea de arquivo, consulte [inicialização instantânea de arquivo](https://technet.microsoft.com/library/ms175935(v=SQL.105).aspx).  
  
