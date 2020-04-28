---
title: Modificar opções de inicialização de instantâneo para Replicação do SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a611de458537156740521dae8b732eed3e2653c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289474"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>Modificar as opções de inicialização de instantâneo para Replicação do SQL

Este artigo discute como modificar várias opções ao [inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md).

## <a name="snapshot-format"></a>Formato do instantâneo
   Especifique o formato do instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  

1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione **SQL Server Nativo – todos os Assinantes devem ser servidores que executam o SQL Server** ou **Caractere – necessário se um Publicador ou Assinante não executar o SQL Server**. 

    > [!NOTE]  
    >  É recomendável a seleção do formato nativo, a menos que essa publicação deva dar suporte a assinaturas de um banco de dados [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ou um banco de dados não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="snapshot-folder-locations"></a>Locais de pasta de instantâneo

### <a name="default-snapshot-location"></a>Localização do instantâneo padrão
Especifique o local do instantâneo padrão (SQL Server Management Studio) especifique o local do instantâneo padrão na página **pasta do instantâneo** do assistente para configurar distribuição. Para obter mais informações sobre como usar o assistente, consulte [Configurar a publicação e a distribuição](configure-publishing-and-distribution.md). Se você criar uma publicação em um servidor que não esteja configurada como Distributor, especifique um local de instantâneo padrão na página **Pasta de Instantâneo** do Assistente para Novas Publicações. Para obter mais informações sobre como usar esse assistente, consulte [Criar uma publicação](publish/create-a-publication.md).  
  
 Modifique o local do instantâneo padrão na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**. Para obter mais informações, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](view-and-modify-distributor-and-publisher-properties.md). Defina a pasta de instantâneo para cada publicação na caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
#### <a name="modify-the-default-snapshot-location"></a>Modificar a localização do instantâneo padrão  
  
1.  Na página **Publicadores** da caixa de diálogo **Propriedades \<do distribuidor –>do distribuidor** , clique no botão de Propriedades (**...**) do Publicador para o qual você deseja alterar o local do instantâneo padrão.    
2.  Na caixa de diálogo **Propriedades do Publicador – \<Publisher>**, digite um valor para a propriedade **Pasta de Instantâneo Padrão**.

    > [!NOTE]  
    >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [proteger a pasta de instantâneo](security/secure-the-snapshot-folder.md).    
1.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

### <a name="alternate-snapshot-location"></a>Local de instantâneo alternativo
  Especificar um local de instantâneo alternativo na página **Instantâneo** da caixa de diálogo **Propriedades de publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md). 

  
#### <a name="specify-an-alternate-snapshot-location"></a>Especificar um local de instantâneo alternativo  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**:    
    1.  Selecione **Colocar os arquivos nesta pasta**, depois clique em **Procurar** para ir para o diretório ou para entrar no caminho de diretório em que os arquivos de instantâneo devem estar armazenados.    

        > [!NOTE]  
        >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [proteger a pasta de instantâneo](security/secure-the-snapshot-folder.md).    
    a.  Desmarque **Colocar os arquivos na pasta padrão** , exceto se for necessário que os arquivos de instantâneo sejam gravados em ambos os locais.    
     Para compactar arquivos de instantâneo, selecione **Compactar arquivos de instantâneo neste local**. A compactação é usada normalmente para conexões de largura da banda baixa e locais de instantâneo alternativos em mídia removível, como um CD-ROM.    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]   


## <a name="compress-snapshot-files"></a>Compactar arquivos de instantâneo
Especifique que os arquivos devem ser compactados na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**:  
  
    1.  Selecione **Colocar os arquivos nesta pasta**, depois clique em **Procurar** para ir para o diretório ou para entrar no caminho de diretório em que os arquivos de instantâneo devem estar armazenados.    
        > [!NOTE]  
        >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [Proteger uma pasta de instantâneo](security/secure-the-snapshot-folder.md)  
  
    2.  Desmarque **Colocar os arquivos na pasta padrão** , exceto se for necessário que os arquivos de instantâneo sejam gravados em ambos os locais.    
        > [!NOTE]  
        >  Se essa caixa de seleção estiver marcada, os arquivos armazenados na pasta padrão não serão compactados. Arquivos compactados só podem ser armazenados no local alternativo especificado na etapa anterior.    
2.  Selecione **Compactar arquivos de instantâneo nesta pasta**.    
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>Executar scripts antes e depois da aplicação do instantâneo

 É possível especificar scripts a serem executados no Assinante antes ou depois que o instantâneo é aplicado. Scripts podem ser usados por várias razões, tais como a criação de logon e esquemas (proprietários de objeto) em cada Assinante.  
  
 Especifica-se um local de arquivo para cada script, e o Agente de Instantâneo copia os arquivos de script para a atual pasta de instantâneo a cada vez que ocorrer o processo de instantâneo. O Agente de Distribuição ou Agente de Mesclagem executa o script pré-instantâneo antes de qualquer script do objeto replicado, ao aplicar um instantâneo. O Agente de Distribuição ou o Agente de Mesclagem executa o script pós-instantâneo depois que todos os outros scripts de objeto e dados replicados tentam sido aplicados. Depois que a aplicação de instantâneo for concluída e os arquivos de script forem executados com êxito, os arquivos de script são removidos do diretório de trabalho no Assinante.  
  
 O script é executado lançando o utilitário **sqlcmd** . Antes de implantar um script, execute-o com **sqlcmd** para assegurar que a execução corra conforme esperado. Os conteúdos de scripts executados antes e depois que o instantâneo é aplicado devem ser repetíveis. Por exemplo, se você criar uma tabela em um script, você deve, em primeiro lugar, verificar sua existência e tomar as ações devidas caso ela exista. O script deve ser repetível, pois se você precisar reinicializar uma assinatura para a qual o script já foi aplicado, o script será aplicado novamente quando o novo instantâneo for aplicado durante a reinicialização.  
  
 Se você estiver compactando o arquivo de instantâneo (colocando-o em um formato de arquivo CAB [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), os scripts também são compactados e colocados no arquivo CAB. Depois que o arquivo de instantâneo compactado for transferido para o Assinante e descompactado para um diretório de trabalho no Assinante, qualquer script indicado como script de pré-instantâneo será executado. Da mesma forma, qualquer script de pós-instantâneo é descompactado e executado no Assinante como última etapa aplicando-se o instantâneo.  

### <a name="execute-a-script-before-or-after-a-snapshot-is-applied"></a>Executar um script antes ou depois de um instantâneo ser aplicado  
 Especifique um script opcional para ser executado antes ou depois da aplicação do instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  


1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**:    
    -   Para especificar um script a ser executado antes de o instantâneo ser aplicado, clique em **Procurar** para navegar até o script ou insira um caminho para o script na caixa de texto **Antes de aplicar o instantâneo, executar este script** . 
   
        > [!NOTE]  
        >  O Agente de Distribuição ou Agente de Mesclagem devem ter permissões de leitura para o diretório especificado. Se forem usadas assinaturas pull, você deverá especificar um diretório compartilhado como um caminho UNC, como \\\computername\scripts\myscript.sql.    
    -   Para especificar um script a ser executado depois de o instantâneo ser aplicado, clique em **Procurar** para navegar até o script ou insira um caminho UNC para o script na caixa de texto **Após aplicar o instantâneo, executar este script** .    
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
  
