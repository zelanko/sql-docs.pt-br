---
title: Mover um UCP de uma instância do SQL Server para outra (Utilitário do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b402fd9e-0bea-4c38-a371-6ed7fea12e96
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b4518884b3fe17ea3a638ed21210775af7c4921c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52793958"
---
# <a name="move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility"></a>Mover um UCP de uma instância do SQL Server para outra (Utilitário do SQL Server)
  Este tópico descreve como usar as etapas a seguir para mover um UCP (ponto de controle do utilitário) de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="move-a-ucp-from-one-instance-of-sql-server-to-another"></a>Mover um UCP de uma instância do SQL Server para outra.  
  
1.  Crie um novo UCP na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que será a nova instância de host do UCP. Para obter mais informações, veja [Criar um ponto de controle do Utilitário do SQL Server &#40;Utilitário do SQL Server&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
2.  Se configurações de política não padrão foram definidas para alguma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility, anote os limites de política para que você possa restabelecê-los no novo UCP. São aplicadas políticas padrão quando são acrescentadas instâncias ao novo UCP. Se políticas padrão forem aplicadas, a exibição de lista do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará **Global** na coluna **Tipo de Política** .  
  
3.  Remova todas as instâncias gerenciadas do UCP antigo. Para obter mais informações, veja [Remover uma instância do SQL Server do Utilitário do SQL Server](remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
4.  Faça backup do data warehouse de gerenciamento do utilitário (UMDW) do UCP antigo. O nome de arquivo é Sysutility_mdw_\<GUID>_DATA e a localização padrão do banco de dados é \<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\, em que \<System drive> geralmente é a unidade C:\. Para obter mais informações, veja [Copiar bancos de dados com Backup e Restauração](../databases/copy-databases-with-backup-and-restore.md).  
  
5.  Restaure o backup do UMDW no novo UCP. Para obter mais informações, veja [Copiar bancos de dados com Backup e Restauração](../databases/copy-databases-with-backup-and-restore.md).  
  
6.  Inscreva instâncias no novo UCP para que elas sejam gerenciadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Para obter mais informações, veja [Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
7.  Implemente definições personalizadas de políticas para as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], conforme o necessário.  
  
8.  Aguarde aproximadamente 1 hora para as operações de coleta de dados e agregação serem concluídas.  
  
9. Para atualizar os dados, clique com o botão direito do mouse no nó **Instâncias Gerenciadas** no **Gerenciador do Utilitário**e selecione **Atualizar**. Os dados de exibição de lista são mostrados no painel de conteúdo do **Gerenciador do Utilitário**. Para obter mais informações, veja [Exibir resultados da política de integridade de recursos &#40;Utilitário do SQL Server&#41;](view-resource-health-policy-results-sql-server-utility.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos e tarefas do Utilitário do SQL Server](sql-server-utility-features-and-tasks.md)   
 [Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
  
