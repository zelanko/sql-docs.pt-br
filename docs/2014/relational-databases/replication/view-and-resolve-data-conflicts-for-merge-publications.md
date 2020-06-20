---
title: Exibir e resolver conflitos de dados para publicações de mesclagem (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 77aa9ece0073149c017f6eca35a756b22751a74b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063671"
---
# <a name="view-and-resolve-data-conflicts-for-merge-publications-sql-server-management-studio"></a>Exibir e resolver conflitos de dados para publicações de mesclagem (SQL Server Management Studio)
  Os conflitos em replicação de mesclagem são resolvidos baseado no resolvedor especificado para cada artigo. Por padrão, os conflitos são resolvidos sem a necessidade da intervenção do usuário. Mas os conflitos podem ser exibidos e o resultado da resolução poderá ser alterado no Visualizador de Conflitos de Replicação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Os dados de conflito são disponíveis no Visualizador de Conflitos de Replicação pelo período de tempo especificado para o período de retenção de conflito (com um padrão de 14 dias). Para definir o período de retenção de conflito, ou:  
  
-   Especifique um valor de retenção para o **@conflict_retention** parâmetro de [sp_addmergepublication &#40;&#41;TRANSACT-SQL ](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql).  
  
-   Especifique um valor de **conflict_retention** para o **@property** parâmetro e um valor de retenção para o **@value** parâmetro de [sp_changemergepublication &#40;&#41;do Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql).  
  
 Por padrão, as informações sobre conflitos são armazenadas:  
  
-   No Publicador e no Assinante, caso o nível de compatibilidade da publicação for 90RTM ou superior.  
  
-   No Publicador, caso o nível de compatibilidade da publicação seja inferior a 80RTM.  
  
-   No Publicador, caso os Assinantes estejam executando [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Os dados de conflito não podem ser armazenados nos Assinantes do [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
 O armazenamento de informações sobre conflitos é controlado pela propriedade de publicação de **conflict_logging** . Para obter mais informações, consulte [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) e [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql).  
  
 Os conflitos também podem ser resolvidos interativamente durante a sincronização usando o Resolvedor Interativo da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . O Resolvedor Interativo está disponível pelo Gerenciador de Sincronização do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Para obter mais informações, consulte [Como sincronizar uma assinatura usando o Gerenciador de Sincronização do Windows &#40;Gerenciador de Sincronização do Windows&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
### <a name="to-view-and-resolve-conflicts-for-merge-publications"></a>Para exibir e resolver conflitos para publicações de mesclagem  
  
1.  Conecte-se ao Publicador (ou assinante, se apropriado) em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e, em seguida, expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação para a qual você quer exibir conflitos e então clique em **Exibir Conflitos**.  
  
    > [!NOTE]  
    >  Se você tiver especificado um valor de **'subscriber'** para a propriedade **conflict_logging** , a opção de menu **Exibir Conflitos** não estará disponível. Para exibir conflitos, inicie o ConflictViewer.exe no prompt de comando. Por padrão, o ConflictViewer.exe está localizado no seguinte diretório: Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE. Para obter uma lista de parâmetros de inicialização válidos, execute o ConflictViewer.exe -?.  
  
4.  Na caixa de diálogo **Selecionar Tabela de Conflito** , selecione um banco de dados, publicação e tabela para os quais quer exibir conflitos.  
  
5.  No Visualizador de Conflitos de Replicação, é possível:  
  
    -   Filtrar linhas com os botões à direita da grade superior.  
  
    -   Selecionar uma linha na grade superior para exibir informações sobre aquela linha na grade inferior.  
  
    -   Selecionar uma ou mais linhas na grade superior e então clicar em **Remover**, que equivale a clicar no botão **Enviar Vencedor** (sem fazer nenhuma alteração nos dados).  
  
    -   Clique no botão de Propriedades (**...**) para exibir mais informações sobre uma coluna envolvida em um conflito.  
  
    -   Edite dados na coluna **Vencedor do Conflito** ou **Perdedor do Conflito** antes de enviar os dados (os dados são de somente leitura se a coluna estiver cinza).  
  
    -   Clique em **Enviar Vencedor** para aceitar a linha designada como o vencedor do conflito.  
  
    -   Clique em **Enviar Perdedor** para substituir a resolução e propagar o valor designado como o perdedor do conflito para todos os nós da topologia.  
  
    -   Selecione **Registrar os detalhes deste conflito** para registrar dados de conflito em um arquivo. Para especificar um local para o arquivo, aponte para o menu **Exibir** e então clique em **Opções**. Insira um valor ou clique no botão procurar (**...**) e então navegue até o arquivo apropriado. Clique em **OK** para sair da caixa de diálogo **Opções** .  
  
6.  Feche o Visualizador de Conflitos de Replicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflitos de replicação de mesclagem avançada](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Especificar um resolvedor de artigo de mesclagem](publish/specify-a-merge-article-resolver.md)  
  
  
