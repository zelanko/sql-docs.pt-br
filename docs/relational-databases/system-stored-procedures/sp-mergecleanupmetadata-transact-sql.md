---
title: sp_mergecleanupmetadata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6924ef36c57036cf6cad6e25a6dc5cebfa5fa5f2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528998"
---
# <a name="spmergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deve ser usado somente em topologias de replicação que incluem servidores que executam versões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. **sp_mergecleanupmetadata** permite que os administradores limpem metadados na **MSmerge_genhistory**, **MSmerge_contents** e **MSmerge_tombstone** tabelas do sistema. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, com um padrão de **%**, que limpa metadados para todas as publicações. A publicação já deve existir se explicitamente especificada.  
  
`[ @reinitialize_subscriber = ] 'subscriber'` Especifica se deve reinicializar o assinante. *assinante* está **nvarchar (5)**, pode ser **verdadeira** ou **FALSE**, com um padrão de **TRUE**. Se **verdadeira**, as assinaturas serão marcadas para reinicialização. Se **falsos**, as assinaturas não são marcadas para reinicialização.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_mergecleanupmetadata** deve ser usado somente em topologias de replicação que incluem servidores que executam versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. Topologias que só incluem o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 ou versão posterior deveriam usar limpeza automática de metadados com base em retenção. Ao executar esse procedimento armazenado, tenha cuidado com o crescimento potencialmente grande e necessário do arquivo de log no computador em que o procedimento armazenado está sendo executado.  
  
> [!CAUTION]
>  Após **sp_mergecleanupmetadata** é executado, por padrão, todas as assinaturas nos assinantes de publicações que têm metadados armazenados no **MSmerge_genhistory**, **MSmerge_contents**  e **MSmerge_tombstone** são marcadas para reinicialização, as alterações pendentes no assinante são perdidas, e o instantâneo atual está marcado como obsoleto.  
> 
> [!NOTE]
>  Se houver várias publicações em um banco de dados e uma dessas publicações usar um período de retenção de publicação infinito (**@retention**=**0**), em execução  **sp_mergecleanupmetadata** não limpará a alteração de replicação de mesclagem metadados para o banco de dados de rastreamento. Por esse motivo, use a retenção de publicação infinita com precaução.  
  
 Ao executar esse procedimento armazenado, você pode optar por reiniciar os assinantes definindo o **@reinitialize_subscriber** parâmetro **verdadeira** (o padrão) ou **FALSE**. Se **sp_mergecleanupmetadata** é executada com o **@reinitialize_subscriber** parâmetro definido como **TRUE**, um instantâneo será reaplicado no assinante, mesmo se a assinatura foi criado sem um instantâneo (por exemplo, se os dados de instantâneo e esquema foram aplicadas manualmente ou já existiam no assinante) inicial. Definindo o parâmetro como **falsos** deve ser usada com cuidado, porque se a publicação não for reiniciada, você deve garantir que os dados no publicador e assinante são sincronizados.  
  
 Independentemente do valor **@reinitialize_subscriber**, **sp_mergecleanupmetadata** processos que estão tentando carregar alterações para um publicador ou assinante de republicação em de mesclagem falhará se não houver em andamento a hora em que o procedimento armazenado é invocado.  
  
 **Executando sp_mergecleanupmetadata com @reinitialize_subscriber = TRUE:**  
  
1.  É recomendado, mas não exigido, que você interrompa todas as atualizações nos bancos de dados de publicação e assinatura. Se a atualização continuar, qualquer atualização feita no Assinante desde a última mesclagem será perdida quando a publicação for reiniciada, mas a convergência dos dados será mantida.  
  
2.  Execute uma mesclagem executando o Agente de Mesclagem. É recomendável que você use o **-validar** opção de linha de comando do agente em cada assinante ao executar o agente de mesclagem. Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
3.  Depois que todas as mesclagens forem concluídas, execute **sp_mergecleanupmetadata**.  
  
4.  Execute **sp_reinitmergepullsubscription** em todos os assinantes usando assinatura pull nomeada ou anônima para garantir a convergência dos dados.  
  
5.  Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
6.  Gere novamente arquivos de instantâneo para todas as publicações de mesclagem envolvidas em todos os níveis. Se tentar fazer a mesclagem sem primeiro gerar novamente o instantâneo, você será solicitado a gerar o instantâneo novamente.  
  
7.  Faça um backup do banco de dados de publicação. Falha nesse procedimento pode causar uma falha de mesclagem depois da restauração de um banco de dados de publicação.  
  
 **Executando sp_mergecleanupmetadata com @reinitialize_subscriber = FALSE:**  
  
1.  Interromper **todas as** atualizações para os bancos de dados de publicação e assinatura.  
  
2.  Execute uma mesclagem executando o Agente de Mesclagem. É recomendável que você use o **-validar** opção de linha de comando do agente em cada assinante ao executar o agente de mesclagem. Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
3.  Depois que todas as mesclagens forem concluídas, execute **sp_mergecleanupmetadata**.  
  
4.  Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
5.  Gere novamente arquivos de instantâneo para todas as publicações de mesclagem envolvidas em todos os níveis. Se tentar fazer a mesclagem sem primeiro gerar novamente o instantâneo, você será solicitado a gerar o instantâneo novamente.  
  
6.  Faça um backup do banco de dados de publicação. Falha nesse procedimento pode causar uma falha de mesclagem depois da restauração de um banco de dados de publicação.  
  
 **Considerações especiais para mesclagens de modo contínuo**  
  
 Se você estiver executando mesclagens do modo contínuo, deverá:  
  
-   Pare o agente de mesclagem e, em seguida, executar outra mesclagem sem o **-contínua** parâmetro especificado.  
  
-   Desativar a publicação com **sp_changemergepublication** para garantir que qualquer mesclagens de modo contínuo que esteja sondando aquele status de publicação falhem.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 Quando você tiver concluído a etapa 3 na execução **sp_mergecleanupmetadata**, retome as mesclagens de modo contínuo com base em como você as interrompeu. Ou:  
  
-   Adicione a **-contínua** parâmetro de volta para o agente de mesclagem.  
  
-   Reative a publicação com **sp_changemergepublication.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_mergecleanupmetadata**.  
  
 Para usar esse procedimento armazenado, o Publicador deve estar executando o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Os assinantes devem estar executando o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, Service Pack 2.  
  
## <a name="see-also"></a>Consulte também  
 [MSmerge_genhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
