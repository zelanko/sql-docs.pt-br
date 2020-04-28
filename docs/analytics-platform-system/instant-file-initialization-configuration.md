---
title: Configurar a inicialização instantânea de arquivo
description: Configurar a inicialização instantânea de arquivo no Analytics Platform System. A inicialização instantânea de arquivo é um recurso SQL Server que permite que as operações de arquivo de dados sejam executadas mais rapidamente.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 83ed373fd4fdd38ae5ddd391678b74e3d2e168c9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401112"
---
# <a name="instant-file-initialization-configuration"></a>Configuração de inicialização de arquivo instantânea
A inicialização instantânea de arquivo é um recurso SQL Server que permite que as operações de arquivo de dados sejam executadas mais rapidamente. Marcar a caixa para ativar a inicialização instantânea de arquivo no irá melhorar o desempenho de SQL Server PDW. No entanto, se isso representar um risco de segurança para sua empresa, deixe a caixa desmarcada.  
  
> [!IMPORTANT]  
> Quando a inicialização instantânea de arquivo está habilitada, SQL Server não substitui bits excluídos por zeros.  Esse comportamento pode criar uma vulnerabilidade de segurança se usuários não autorizados obterem acesso a dados excluídos. No entanto, SQL Server PDW atenua esse risco, garantindo que o banco de dados SQL Server e os arquivos de backup estejam sempre anexados a uma instância do SQL Server; somente a conta de serviço SQL Server e o administrador local podem acessar os dados excluídos no SQL Server PDW.  
  
A inicialização instantânea de arquivo não está disponível quando a TDE está habilitada.  
  
## <a name="add-permission-for-the-backup-account"></a>Adicionar permissão para a conta de backup  
O processo de backup requer uma credencial de rede (conta de usuário do Windows) que possa acessar o local de armazenamento de backup. Você autoriza o PDW a usar a conta usando o procedimento [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) . Consulte [backup Database](../t-sql/statements/backup-database-parallel-data-warehouse.md) para todo o processo de backup. Para usar a inicialização instantânea de arquivo, a conta de backup deve `Perform volume maintenance tasks` receber a permissão.  
  
1.  No servidor de backup, abra o aplicativo de **política de segurança local** (`secpol.msc`).  
  
2.  No painel esquerdo, expanda **Políticas Locais**e, em seguida, clique em **Atribuição de Direitos de Usuário**.  
  
3.  No painel direito, clique duas vezes em **Executar tarefas de manutenção de volume**.  
  
4.  Clique em **Adicionar Usuário ou Grupo** e adicione as contas de usuário que são usadas ​​para backups.  
  
5.  Clique em **Aplicar**e feche todas as caixas de diálogo **Política de Segurança Local** .  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>Para ativar ou desativar a inicialização instantânea de arquivo  
  
1.  Inicie o Configuration Manager. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;&#41;do sistema de plataforma de análise ](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo da Configuration Manager, clique em **inicialização instantânea de arquivo**.  
  
3.  Para ativar a inicialização instantânea de arquivo, selecione a caixa ao lado de **habilitar a inicialização instantânea de arquivo em todos os nós**. Para desativar a inicialização instantânea de arquivo, desmarque a caixa ao lado de **habilitar a inicialização instantânea de arquivo em todos os nós**.  
  
    > [!WARNING]  
    > Quando você desativa a inicialização instantânea de arquivo, a consideração de segurança discutida acima para o recurso ainda pode se aplicar a arquivos excluídos enquanto a inicialização instantânea de arquivo estava habilitada.  
  
4.  Clique em **Aplicar**. A alteração será propagada por meio das instâncias de SQL Server em SQL Server PDW na próxima vez em que os serviços do dispositivo forem reiniciados. Para reiniciar os serviços de dispositivo agora, consulte [status dos serviços do PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).  
  
5.  Talvez você queira repetir as etapas descritas acima como **adicionar permissão para a conta de backup** para remover a permissão **executar tarefas de manutenção de volume** .  
  
![Inicialização de arquivo instantâneo PDW do dispositivo DWConfig](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
Para obter mais informações sobre a inicialização instantânea de arquivo, consulte [inicialização instantânea de arquivo](https://technet.microsoft.com/library/ms175935(v=SQL.105).aspx).  
  
