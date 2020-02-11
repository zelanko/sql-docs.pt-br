---
title: Configurações de backup de log de transações de envio de logs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.logshipping.settings.tlogback.f1
ms.assetid: 9a6e6c16-7f71-412b-bba6-7bffac001277
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d2e1484107e4ee5e7f7f2a10eaa719b5c96c098e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62916884"
---
# <a name="log-shipping-transaction-log-backup-settings"></a>Configurações de backup de log de transações do envio de log
  Use esta caixa de diálogo para configurar e modificar as configurações de backup de log de transações para o envio de log  
  
 Para obter uma explicação dos conceitos de envio de log, veja [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opções  
 **Caminho de rede para a pasta de backup**  
 Nesta caixa, digite o compartilhamento de rede para a sua pasta de backup. A pasta local onde os seus backups de log de transações são salvos deve ser compartilhada para que os trabalhos de cópia do envio de log possam copiar esses arquivos para o servidor secundário. Você deve conceder permissões de leitura para este compartilhamento de rede na conta proxy sob a qual o trabalho de cópia será executado na instância do servidor secundário. Por padrão, esta é a conta do serviço SQLServerAgent da instância do servidor secundário, mas o administrador pode selecionar uma outra conta proxy para o trabalho.  
  
 **Se a pasta de backup estiver localizada n servidor primário, digite o caminho local para a pasta**  
 Digite a letra da unidade local e o caminho para a pasta de backup se esta pasta estiver localizada no servidor primário Se a pasta de backup não estiver localizada no servidor primário, deixe isto em branco  
  
 Se especificar um caminho local aqui, o comando BACKUP usará este caminho para criar os backups de log de transações; do contrário, se nenhum caminho local for especificado, o comando BACKUP usará o caminho de rede especificado na caixa **Caminho de rede para a pasta de backup** .  
  
> [!NOTE]  
>  Se a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver executando sob a conta Sistema Local no servidor primário, você deverá criar a pasta de backup no servidor primário e especificar o caminho local para aquela pasta aqui. A conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da instância do servidor primário deve ter permissões de Leitura e Gravação nessa pasta.  
  
 **Excluir arquivos mais antigos que**  
 Especifique o período de tempo que deseja que os backups de log de transações permaneçam no seu diretório de backup antes de serem excluídos.  
  
 **Alertar se nenhum backup ocorrer dentro de**  
 Especifique o período de tempo que você deseja que o envio de log espere antes de acionar um alerta de que nenhum backup de log de transações ocorreu.  
  
 **Nome do trabalho**  
 Exibe o nome do trabalho do SQL Server Agent usado para criar os backups de log de transação para envio de logs. Quando for criar o trabalho pela primeira vez, você pode modificar o nome digitando-o na caixa.  
  
 **Agenda**  
 Exibe o cronograma atual para realizar o backup dos logs de transações do banco de dados primário. Antes de criar o o trabalho de backup, você pode modificar este cronograma clicando em **Cronograma...** . Após a criação do trabalho, você pode modificar este cronograma clicando em **Editar Trabalho...** .  
  
### <a name="backup-job"></a>Trabalho de backup  
 **Agenda....**  
 Modificar o cronograma que foi criado quando o trabalho do SQL Server Agent foi criado  
  
 **Editar Trabalho...**  
 Modifique os parâmetros do trabalho do SQL Server Agent para o trabalho que realiza os backups de log de transações no banco de dados primário.  
  
 **Desabilitar este trabalho**  
 Desabilite o trabalho do SQL Server Agent para impedir a criação de backups de log de transações.  
  
### <a name="compression"></a>Compactação  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou uma versão posterior) dá suporte à [compactação de backup](../backup-restore/backup-compression-sql-server.md).  
  
 **Defina compactação de backup**  
 No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou uma versão posterior), selecione um dos seguintes valores de compactação de backup para os backups dos logs desta configuração de envio de logs:  
  
|||  
|-|-|  
|**Usar a configuração padrão do servidor**|Clique para usar o padrão do nível de servidor.<br /><br /> Esse padrão é definido pela opção de configuração do servidor **padrão de compactação de backup** . Para obter informações sobre como exibir a configuração atual dessa opção, consulte [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
|**Compactar backup**|Clique em compactar backup, independentemente do padrão do nível do servidor.<br /><br /> **\*\* Importante \*\*** Por padrão, a compactação aumenta consideravelmente o uso da CPU, e o consumo adicional da CPU por parte do processo de compactação poderá afetar negativamente as operações simultâneas. Portanto, convém criar backups compactados de baixa prioridade em uma sessão cujo uso da CPU é limitado pelo [Administrador de Recursos](../resource-governor/resource-governor.md). Para obter mais informações, consulte [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).|  
|**Não compactar o backup**|Clique em criar um backup não compactado, independentemente do padrão do nível do servidor.|  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um usuário para criar e gerenciar trabalhos do SQL Server Agent](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)   
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
