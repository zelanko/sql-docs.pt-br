---
title: sp_mergecleanupmetadata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 21740d0105f07e4792fbaff90ebb73b4dda3d338
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spmergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deve ser usado somente em topologias de replicação que incluem servidores que executam versões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. **sp_mergecleanupmetadata** permite que os administradores limpem metadados no **MSmerge_genhistory**, **MSmerge_contents** e **MSmerge_tombstone** tabelas do sistema. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão de **%**, que limpa metadados para todas as publicações. A publicação já deve existir se explicitamente especificada.  
  
 [  **@reinitialize_subscriber =** ] **'***assinante***'**  
 Especifica se o Assinante deve ser reinicializado. *assinante* é **nvarchar (5)**, pode ser **TRUE** ou **FALSE**, com um padrão de **TRUE**. Se **TRUE**, as assinaturas serão marcadas para reinicialização. Se **FALSE**, as assinaturas não estão marcadas para reinicialização.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_mergecleanupmetadata** deve ser usado somente em topologias de replicação que incluem servidores que executam versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. Topologias que só incluem o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 ou versão posterior deveriam usar limpeza automática de metadados com base em retenção. Ao executar esse procedimento armazenado, tenha cuidado com o crescimento potencialmente grande e necessário do arquivo de log no computador em que o procedimento armazenado está sendo executado.  
  
> [!CAUTION]  
>  Depois de **sp_mergecleanupmetadata** é executado, por padrão, todas as assinaturas nos assinantes de publicações com metadados armazenados em **MSmerge_genhistory**, **MSmerge_contents**  e **MSmerge_tombstone** são marcadas para reinicialização, as alterações pendentes no assinante são perdidas, e o instantâneo atual está marcado como obsoleto.  
  
> [!NOTE]  
>  Se houver várias publicações em um banco de dados e qualquer uma dessas publicações usar um período de retenção de publicação infinito (**@retention**=**0**), executando  **sp_mergecleanupmetadata** não limpará a alteração de replicação de mesclagem metadados para o banco de dados de rastreamento. Por esse motivo, use a retenção de publicação infinita com precaução.  
  
 Ao executar esse procedimento armazenado, você pode optar por reiniciar os assinantes definindo o **@reinitialize_subscriber** parâmetro **TRUE** (o padrão) ou **FALSE**. Se **sp_mergecleanupmetadata** é executada com o **@reinitialize_subscriber** parâmetro definido como **TRUE**, um instantâneo será reaplicado no assinante, mesmo que a assinatura foi criado sem um instantâneo (por exemplo, se os dados de instantâneo e esquema foram aplicados manualmente ou já existiam no assinante) inicial. Definindo o parâmetro como **FALSE** deve ser usada com cuidado, porque se a publicação não for reiniciada, você deve garantir que os dados no publicador e assinante estão sincronizados.  
  
 Independentemente do valor **@reinitialize_subscriber**, **sp_mergecleanupmetadata** processos que estão tentando carregar alterações para um publicador ou um assinante de republicação de mesclagem falhará se houver em andamento a hora em que o procedimento armazenado é chamado.  
  
 **Executando sp_mergecleanupmetadata com @reinitialize_subscriber = TRUE:**  
  
1.  É recomendado, mas não exigido, que você interrompa todas as atualizações nos bancos de dados de publicação e assinatura. Se a atualização continuar, qualquer atualização feita no Assinante desde a última mesclagem será perdida quando a publicação for reiniciada, mas a convergência dos dados será mantida.  
  
2.  Execute uma mesclagem executando o Agente de Mesclagem. Recomendamos que você use o **– validar** opção de linha de comando do agente em cada assinante ao executar o Merge Agent. Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
3.  Depois que todas as mesclagens forem concluídas, execute **sp_mergecleanupmetadata**.  
  
4.  Executar **sp_reinitmergepullsubscription** em todos os assinantes usando assinatura pull nomeada ou anônima para garantir a convergência de dados.  
  
5.  Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
6.  Gere novamente arquivos de instantâneo para todas as publicações de mesclagem envolvidas em todos os níveis. Se tentar fazer a mesclagem sem primeiro gerar novamente o instantâneo, você será solicitado a gerar o instantâneo novamente.  
  
7.  Faça um backup do banco de dados de publicação. Falha nesse procedimento pode causar uma falha de mesclagem depois da restauração de um banco de dados de publicação.  
  
 **Executando sp_mergecleanupmetadata com @reinitialize_subscriber = FALSE:**  
  
1.  Parar **todas as** atualizações para os bancos de dados de publicação e assinatura.  
  
2.  Execute uma mesclagem executando o Agente de Mesclagem. Recomendamos que você use o **– validar** opção de linha de comando do agente em cada assinante ao executar o Merge Agent. Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
3.  Depois que todas as mesclagens forem concluídas, execute **sp_mergecleanupmetadata**.  
  
4.  Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
5.  Gere novamente arquivos de instantâneo para todas as publicações de mesclagem envolvidas em todos os níveis. Se tentar fazer a mesclagem sem primeiro gerar novamente o instantâneo, você será solicitado a gerar o instantâneo novamente.  
  
6.  Faça um backup do banco de dados de publicação. Falha nesse procedimento pode causar uma falha de mesclagem depois da restauração de um banco de dados de publicação.  
  
 **Considerações especiais para mesclagens de modo contínuo**  
  
 Se você estiver executando mesclagens do modo contínuo, deverá:  
  
-   Parar o agente de mesclagem e, em seguida, executar outra mesclagem sem o **-contínua** parâmetro especificado.  
  
-   Desativar a publicação com **sp_changemergepublication** para certificar-se de que qualquer mesclagens de modo contínuo que esteja sondando o status da publicação.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 Quando você concluiu a etapa 3 na execução **sp_mergecleanupmetadata**, retome as mesclagens de modo contínuo com base em como você as interrompeu. Ou:  
  
-   Adicionar o **– Continuous** parâmetro de volta para o agente de mesclagem.  
  
-   Reative a publicação com **sp_changemergepublication.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_mergecleanupmetadata**.  
  
 Para usar esse procedimento armazenado, o Publicador deve estar executando o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Os assinantes devem estar executando o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, Service Pack 2.  
  
## <a name="see-also"></a>Consulte também  
 [MSmerge_genhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
