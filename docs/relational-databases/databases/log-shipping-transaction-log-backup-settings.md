---
title: "Configurações de backup de log de transações de envio de logs | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: log-shipping
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.tlogback.f1
ms.assetid: 9a6e6c16-7f71-412b-bba6-7bffac001277
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01a15e3ebf54cae459aad00052e009774d125c56
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="log-shipping-transaction-log-backup-settings"></a>Configurações de backup de log de transações do envio de log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use esta caixa de diálogo para configurar e modificar as definições de backup de log de transações de uma configuração de envio de logs.  
  
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
 Exibe o cronograma atual para realizar o backup dos logs de transações do banco de dados primário. Antes de criar o o trabalho de backup, você pode modificar este cronograma clicando em **Cronograma...**. Após a criação do trabalho, você pode modificar este cronograma clicando em **Editar Trabalho...**.  
  
### <a name="backup-job"></a>Trabalho de backup  
 **Cronograma...**  
 Modificar o cronograma que foi criado quando o trabalho do SQL Server Agent foi criado  
  
 **Editar Trabalho...**  
 Modifique os parâmetros do trabalho do SQL Server Agent para o trabalho que realiza os backups de log de transações no banco de dados primário.  
  
 **Desabilitar este trabalho**  
 Desabilite o trabalho do SQL Server Agent para impedir a criação de backups de log de transações.  
  
### <a name="compression"></a>Compactação  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou uma versão posterior) dá suporte à [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
 **Defina compactação de backup**  
 No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou uma versão posterior), selecione um dos seguintes valores de compactação de backup para os backups dos logs desta configuração de envio de logs:  
  
|||  
|-|-|  
|**Usar a configuração padrão do servidor**|Clique para usar o padrão do nível de servidor.<br /><br /> Esse padrão é definido pela opção de configuração do servidor **padrão de compactação de backup** . Para obter informações sobre como exibir a configuração atual dessa opção, consulte [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
|**Compactar backup**|Clique em compactar backup, independentemente do padrão do nível do servidor.<br /><br /> **\*\* Importante \*\*** Por padrão, a compactação aumenta consideravelmente o uso da CPU, e o consumo adicional da CPU por parte do processo de compactação poderá afetar negativamente as operações simultâneas. Portanto, convém criar backups compactados de baixa prioridade em uma sessão cujo uso da CPU é limitado pelo [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md). Para obter mais informações, consulte [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).|  
|**Não compactar o backup**|Clique em criar um backup não compactado, independentemente do padrão do nível do servidor.|  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um usuário para criar e gerenciar trabalhos do SQL Server Agent](http://msdn.microsoft.com/library/67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef)   
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
