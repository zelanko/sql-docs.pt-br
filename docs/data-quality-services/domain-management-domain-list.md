---
title: "Gerenciamento de domínio: lista de domínios | Microsoft Docs"
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dqs.dm.domainlist.f1
ms.assetid: 8df305f0-97ea-4226-811b-979ed862e1f0
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36d7b173e7199cdffd50841360731fcc81f4fd43
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="domain-management-domain-list"></a>Gerenciamento de domínio: lista de domínios
  Este tópico descreve os controles na lista Domínios da página **Gerenciamento de Domínio** no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Use este painel para selecionar um domínio no qual poderá executar operações de gerenciamento. O mesmo painel é usado para todas as páginas tabuladas na página **Gerenciamento de Domínio** .  
  
## <a name="options"></a>Opções  
  
### <a name="domains-list"></a>Lista de domínios  
 **Domínio**  
 Esta lista mostra todos os domínios na base de dados de conhecimento. Operações que você executa nas páginas tabuladas no painel direito serão executadas no domínio que é selecionado na lista. Para obter mais informações, consulte  
  
 **Criar um domínio composto**  
 Crie um novo domínio composto na base de dados de conhecimento. Este comando exibirá a caixa de diálogo **Criar um domínio composto** . Para disponibilizar este comando, clique com o botão direito do mouse em um domínio ou clique no ícone acima da lista de domínios. Para obter mais informações, consulte [Criar um domínio composto](../data-quality-services/create-a-composite-domain.md).  
  
 **Criar um domínio**  
 Crie um novo domínio na base de dados de conhecimento. Este comando exibirá a caixa de diálogo **Criar Domínio** . Para disponibilizar este comando, clique com o botão direito do mouse em um domínio ou clique no ícone acima da lista de domínios. Para obter mais informações, consulte [Criar um domínio](../data-quality-services/create-a-domain.md).  
  
 **Criar uma cópia do domínio selecionado**  
 Crie uma cópia exata do domínio selecionado e adicione-a à base de dados de conhecimento. O nome da cópia será o nome do domínio que a originou, mais " – Cópia" anexado ao nome. Para disponibilizar este comando, clique com o botão direito do mouse em um domínio e clique em **Criar uma cópia**, ou clique no ícone acima da lista de domínios. Ele não está disponível para um domínio composto.  
  
 **Importar domínio de arquivo de dados**  
 Importe um domínio de um arquivo .dqs. Este comando exibe a caixa de diálogo **Importar do Arquivo de Dados** que o permite procurar o sistema de arquivos e selecionar um arquivo .dqs para um único domínio ou um domínio composto. Para disponibilizar este comando, clique no ícone acima da lista de domínios. Para obter mais informações, consulte [Importe um domínio de um arquivo .dqs](../data-quality-services/import-a-domain-from-a-dqs-file.md).  
  
 **Excluir domínio**  
 Exclua o domínio selecionado da base de dados de conhecimento. Este comando exibe a caixa de diálogo **SQL Server Data Quality Services** . Se você clicar em **Sim**, o domínio e todos os seus dados serão excluídos permanentemente. Para disponibilizar este comando, clique com o botão direito do mouse em um domínio ou clique no ícone acima da lista de domínios.  
  
 **Criar um domínio vinculado**  
 Crie um domínio que seja vinculado ao domínio selecionado. Este comando exibe a caixa de diálogo **Criar domínio** . Para disponibilizar este comando, clique com o botão direito do mouse em um domínio e clique em **Criar um Domínio Vinculado** que está vinculado ao domínio selecionado. O domínio ao qual você está se vinculando é mostrado na caixa de diálogo Criar Domínio. O comando não está disponível para um domínio composto. Não há comando disponível para desvincular dois domínios; para fazer isso, exclua o domínio vinculado. Não é possível criar um domínio vinculado para outro domínio vinculado. Para obter mais informações, consulte [Criar um Domínio Vinculado](../data-quality-services/create-a-linked-domain.md).  
  
 Um domínio vinculado tem os mesmos valores que o domínio ao qual ele está vinculado. Apenas o nome e as propriedades do domínio são diferentes. Se você alterar uma regra de domínio, um valor de domínio, um vínculo de dados de referência ou uma relação baseada em termos no domínio ao qual está vinculado, a regra de domínio, o valor de domínio, o vínculo de dados de referência ou a relação baseada em termos no domínio vinculado também será alterada. Além disso, se você alterar um valor no domínio vinculado, a alteração também será feita no domínio vinculado.  
  
 **Exportar base de dados de conhecimento**  
 Exporte a base de dados de conhecimento inteira para um arquivo .dqs. Este comando exibe a caixa de diálogo **Exportar para Arquivo de Dados** . Para disponibilizar este comando, clique no ícone **Exportar dados da Base de Dados de Conhecimento** na parte superior da página, ou em **Exportar** no menu de contexto dos domínios no painel de lista de domínios. Para obter mais informações, consulte [Exportar uma base de dados de conhecimento para um arquivo .dqs](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md).  
  
 **Exportar domínio**  
 Exporte o domínio para um arquivo .dqs. Este comando exibe a caixa de diálogo **Exportar para Arquivo de Dados** . Para disponibilizar este comando, clique no menu **Exportar** da barra de menus, na parte superior da página, ou clique com o botão direito do mouse no painel de lista de domínios. Para obter mais informações, consulte [Exportar um domínio para um arquivo .dqs](../data-quality-services/export-a-domain-to-a-dqs-file.md).  
  
  
