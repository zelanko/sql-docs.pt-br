---
title: Fazer backup de banco de dados (página Opções de Backup) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdatabase.options.f1
- swb.backupdatabase.options.f1
ms.assetid: df0ddcdb-c94e-472b-b786-469ae8117b93
caps.latest.revision: 61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b37c533d269885ce60da9ffe66eaa766222442d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37175903"
---
# <a name="back-up-database-backup-options-page"></a>Backup de Banco de Dados (página Opções de Backup)
  Use a página  **Opções de Backup** da caixa de diálogo **Backup de Banco de Dados** para exibir ou modificar opções de backup de banco de dados.  
  
 **Para criar um backup usando o SQL Server Management Studio**  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  Você pode definir um plano de manutenção de banco de dados para criar backups de banco de dados. Para obter mais informações, consulte [Planos de Manutenção](../maintenance-plans/maintenance-plans.md) e [Usar o Assistente de Plano de Manutenção](../maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
> [!NOTE]  
>  Ao especificar uma tarefa de backup usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é possível gerar o script [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) correspondente clicando no botão **Script** e selecionando um destino para o script.  
  
## <a name="options"></a>Opções  
  
### <a name="backup-set"></a>Conjunto de backup  
 As opções do painel **Conjunto de backup** permitem especificar informações opcionais sobre o conjunto de backup criado pela operação de backup.  
  
 **Nome**  
 Especifique o nome do conjunto de backup. O sistema sugere automaticamente um nome padrão com base no nome do banco de dados e no tipo de backup.  
  
 Para obter informações sobre conjuntos de backup, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
 **Descrição**  
 Insira uma descrição do conjunto de backup.  
  
 **O conjunto de backup vai expirar**  
 Escolha uma das opções de validade a seguir. Essa opção será desabilitada se a opção **URL** for escolhida como destino do backup.  
  
|||  
|-|-|  
|**After (após)**|Especifique o número de dias que devem decorrer antes de o conjunto de backup expirar e poder ser substituído. Esse valor pode ser de 0 a 99999 dias; 0 dia significa que o conjunto de backup nunca vai expirar.<br /><br /> O valor padrão de validade do backup é o valor definido na opção **Retenção de mídia de backup padrão (em dias)** . Para acessá-la, clique com o botão direito do mouse no nome do servidor no Pesquisador de Objetos e selecione **Propriedades**; em seguida, clique na página **Definições de banco de dados** da caixa de diálogo **Propriedades do servidor** .|  
|**Em**|Defina uma data específica em que o conjunto de backup deverá expirar e poderá ser substituído.|  
  
### <a name="compression"></a>Compactação  
 [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] (ou uma versão posterior) dá suporte à [compactação de backup](backup-compression-sql-server.md).  
  
 **Defina compactação de backup**  
 No [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] (ou em uma versão posterior), selecione um dos seguintes valores de compactação de backup:  
  
|||  
|-|-|  
|**Usar a configuração padrão do servidor**|Clique para usar o padrão do nível de servidor.<br /><br /> Esse padrão é definido pela opção de configuração do servidor **padrão de compactação de backup** . Para obter informações sobre como exibir a configuração atual dessa opção, consulte [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
|**Compactar backup**|Clique em compactar backup, independentemente do padrão do nível do servidor.<br /><br /> **\*\* Importante \*\*** Por padrão, a compactação aumenta consideravelmente o uso da CPU, e o consumo adicional da CPU por parte do processo de compactação poderá afetar negativamente as operações simultâneas. Portanto, é recomendável criar backups compactados de baixa prioridade em uma sessão cujo uso da CPU é limitado pelo [Administrador de Recursos](../resource-governor/resource-governor.md). Para obter mais informações, consulte [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).|  
|**Não compactar o backup**|Clique em criar um backup não compactado, independentemente do padrão do nível do servidor.|  
  
### <a name="encryption"></a>Criptografia  
 Para criar um backup criptografado, marque a caixa de seleção **Criptografar backup** . Selecione um algoritmo de criptografia a ser usado na etapa de criptografia e forneça um Certificado ou uma Chave assimétrica de uma lista de certificados ou chaves assimétricas existentes. Os algoritmos de criptografia disponíveis são:  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   Triple DES  
  
> [!TIP]  
>  A opção de criptografia estará desabilitada se você optou por anexar ao conjunto de backup existente.  
>   
>  É prática recomendada fazer backup do certificado ou das chaves e armazená-los em um local diferente do backup que você criptografou.  
>   
>  Há suporte somente para as chaves que residem no EKM (Gerenciamento Extensível Chaves).  
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Fazer backup de um log de transações &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [Fazer backup do log de transações quando o banco de dados está danificado &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
