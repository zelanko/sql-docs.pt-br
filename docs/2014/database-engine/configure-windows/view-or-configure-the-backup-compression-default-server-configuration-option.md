---
title: Exibir ou configurar a opção de configuração de servidor backup compression default | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], backup compression default option
- backup compression [SQL Server], backup compression default Option
ms.assetid: 23029395-3e93-4c29-b7d6-e5a47a3526ff
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7907a8e1187169c8c7581e3ad5f81eef2dde15b2
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640727"
---
# <a name="view-or-configure-the-backup-compression-default-server-configuration-option"></a>Exibir ou configurar a opção de configuração de servidor backup compression default
  Este tópico descreve como exibir ou configurar a opção de configuração de servidor **padrão de compactação de backup** em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção de **padrão de compactação de backup** determina se a instância de servidor cria backups compactados por padrão. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado, a opção de **padrão de compactação de backup** está desativada.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para exibir ou configurar a opção padrão de compactação de backup usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [Depois de configurar a opção backup compression default](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
  
-   A compactação de backup não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   Por padrão, a compactação aumenta consideravelmente o uso da CPU, e o consumo adicional da CPU por parte do processo de compactação pode afetar negativamente as operações simultâneas. Portanto, é recomendável criar backups compactados de baixa prioridade em uma sessão cujo uso da CPU é limitado pelo [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md). Para obter mais informações, consulte [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Ao criar um backup individual, definir uma configuração de envio de logs ou criar um plano de manutenção, é possível substituir o padrão do nível de servidor.  
  
-   Compactação de backup tem suporte tanto para dispositivos de backup de disco como para dispositivos de backup de fita.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-configure-the-backup-compression-default-option"></a>Para exibir ou configurar a opção padrão de compactação de backup  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Configurações de Banco de Dados** .  
  
3.  Em **Backup e restauração**, **Compactar backup** mostra a configuração atual da opção de **padrão de compactação de backup** . Essa configuração determina o padrão do nível de servidor para backups compactados, como segue:  
  
    -   Se a caixa **Compactar backup** estiver em branco, novos backups são descompactados por padrão.  
  
    -   Se a caixa **Compactar backup** estiver marcada, novos backups serão compactados por padrão.  
  
     Se você for membro da função de servidor fixa **sysadmin** ou **serveradmin** , também será possível alterar a configuração padrão clicando na caixa **Compactar backup** .  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-view-the-backup-compression-default-option"></a>Para exibir a opção padrão de compactação de backup  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo consulta a exibição de catálogo [sys.configurations](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql) para determinar o valor de `backup compression default`. O valor 0 significa que a compactação de backup está desativada e o valor 1 significa que a compactação de backup está habilitada.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
SELECT value   
FROM sys.configurations   
WHERE name = 'backup compression default' ;  
GO  
  
```  
  
#### <a name="to-configure-the-backup-compression-default-option"></a>Para configurar a opção padrão de compactação de backup  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para configurar a instância de servidor para criar backups compactados por padrão.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_configure 'backup compression default', 1 ;  
RECONFIGURE WITH OVERRIDE ;  
GO  
  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhar: Depois de configurar a opção backup compression default  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  
