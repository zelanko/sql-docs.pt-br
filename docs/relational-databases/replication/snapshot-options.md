---
title: Modificar as opções de inicialização de instantâneo
description: Modifique várias opções de inicialização de instantâneo de Replicação, como o formato de instantâneo e o local da pasta de instantâneo no SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3117e274c146413dcf8b973f054c7d0b1865e7de
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767604"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>Modificar as opções de inicialização de instantâneo para Replicação do SQL 
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Há várias opções disponíveis para especificar ao [inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md).

## <a name="specify-snapshot-format-sql-server-management-studio"></a>Especificar o formato do instantâneo (SQL Server Management Studio)
  Especifique o formato do instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades de Publicação – \<Publication>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-specify-snapshot-format"></a>Para especificar o formato do instantâneo  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publication>** , selecione **SQL Server Nativo – todos os Assinantes devem ser servidores que executam o SQL Server** ou **Caractere – necessário se um Editor ou Assinante não executar o SQL Server**.  
  
    > [!NOTE]  
    >  É recomendável a seleção do formato nativo, a menos que essa publicação deva dar suporte a assinaturas de um banco de dados do SQL Server Compact ou um banco de dados não SQL Server.  
  
2.  Selecione **OK**.   

## <a name="snapshot-folder-locations"></a>Locais de pasta de instantâneo

### <a name="default-snapshot-location"></a>Localização do instantâneo padrão
Especifique o local de instantâneo padrão na página **Pasta de Instantâneo** do Assistente para Configurar Distribuição. Para obter mais informações sobre como usar o assistente, consulte [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md). Se você criar uma publicação em um servidor que não esteja configurada como Distributor, especifique um local de instantâneo padrão na página **Pasta de Instantâneo** do Assistente para Novas Publicações. Para obter mais informações sobre como usar esse assistente, consulte [Criar uma publicação](../../relational-databases/replication/publish/create-a-publication.md).  
  
 Modifique a localização do instantâneo padrão na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** . Para obter mais informações, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md). Defina a pasta de instantâneo para cada publicação na caixa de diálogo **Propriedades da Publicação – \<Publication>** . Para obter mais informações, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-modify-the-default-snapshot-location"></a>Para modificar o local do instantâneo padrão.  
  
1.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** , clique no botão de propriedades ( **...** ) para o Publicador para o qual você deseja alterar a localização do instantâneo padrão.    
2.  Na caixa de diálogo **Propriedades do Editor –\<Publisher>** , digite um valor para a propriedade **Pasta de Instantâneo Padrão**.  
  
    > [!NOTE]  
    >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md).    
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
 

### <a name="alternate-snapshot-locations"></a>Locais de instantâneo alternativos
Locais de instantâneos alternativos permitem que você armazene arquivos de instantâneos em outro local ou em local diferente do padrão onde normalmente está localizado no Distribuidor. Locais alternativos podem ficar em outro servidor, em uma unidade de rede ou uma mídia removível (como um CD-ROM ou disco removível).  
  
Locais de instantâneo alternativos são armazenados como uma propriedade da publicação. Devido ao local de instantâneo alternativo ser uma propriedade da publicação, o Agente de Distribuição e o Agente de Mesclagem podem localizar o instantâneo apropriado como parte do processo de sincronização.  
  
Para especificar um local de pasta de instantâneo padrão ou compactar arquivos de instantâneo, crie a publicação sem criar o instantâneo inicial imediatamente, defina as propriedades da publicação para o local do instantâneo e execute o Agente de Instantâneo para aquela publicação. Se você alterar o local alternativo após criar o instantâneo inicial, o local de qualquer instantâneo gerado para a publicação não será realocado para o novo local alternativo. Nesse caso, dependendo das configurações da publicação, o Merge Agent ou Distribution Agent talvez não encontrem os arquivos de instantâneo no novo local alternativo.  
  
> [!NOTE]  
>  Não especifique nenhum local alternativo (usando a caixa de diálogo **Propriedades da Publicação** ou [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)) que seja igual ao local da pasta do instantâneo padrão.  
  
> [!CAUTION]  
>  Não use WebSync e locais de pasta de instantâneo alternativos ao mesmo tempo.  
  
#### <a name="use-sql-server-management-studio"></a>Usar o SQL Server Management Studio
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publication>** :  
  
    1.  Selecione **Colocar os arquivos nesta pasta**, depois clique em **Procurar** para ir para o diretório ou para entrar no caminho de diretório em que os arquivos de instantâneo devem estar armazenados.  
  
        > [!NOTE]  
        >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    2.  Desmarque **Colocar os arquivos na pasta padrão** , exceto se for necessário que os arquivos de instantâneo sejam gravados em ambos os locais.  
  
     Para compactar arquivos de instantâneo, selecione **Compactar arquivos de instantâneo neste local**. A compactação é usada normalmente para conexões de largura da banda baixa e locais de instantâneo alternativos em mídia removível, como um CD-ROM.  
  
2.  Selecione **OK**.  
  
#### <a name="use-transact-sql"></a>Usar o Transact-SQL 

Ao [Configurar Propriedades de Instantâneo &#40;Programação Transact-SQL de Replicação&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md), especifique o valor para **snapshot_in_defaultfolder** como false. 

## <a name="compressed-snapshots"></a>Instantâneos compactados
  A compactação de arquivos de instantâneo é apropriada quando se está transferindo instantâneos por uma rede lenta ou salvando-os em mídia removível e um instantâneo não compactado é grande demais para a mídia. A compactação de arquivos de instantâneo é útil nessas situações, mas a compactação aumenta o tempo para gerar e aplicar o instantâneo.  
  
 Arquivos de instantâneo compactados são gravados no formato de arquivo CAB [!INCLUDE[msCoName](../../includes/msconame-md.md)] , capaz de compactar arquivos de 2 GB ou menos (se os arquivos de instantâneo forem maiores do que 2GB, eles não podem ser compactados). Para compactar arquivos, eles precisam ser gravados em uma pasta de instantâneo alternativa (arquivos gravados na pasta de instantâneo padrão não podem ser compactados). 
  
 Arquivos são descompactados no local onde o Distribuition Agent ou Agente de Mesclagem são executados; assinaturas pull são geralmente usadas com instantâneos compactados para que os arquivos sejam descompactados no Assinante. Quando o Assinante recebe um arquivo compactado, o arquivo é inicialmente gravado em um local temporário. Depois que o arquivo compactado é copiado para o Assinante, os arquivos de instantâneo no arquivo compactado são descompactados, em ordem, um arquivo de cada vez pelo utilitário CAB. O espaço exigido no Assinante é o tamanho do arquivo compactado mais o arquivo não comprimido maior.  
  
> [!NOTE]  
>  Os instantâneos compactados podem, em alguns casos, melhorar o desempenho da transferência de arquivos de instantâneo pela rede. No entanto, a compactação de instantâneos exige processamento adicional por parte do Snapshot Agent ao gerar os arquivos de instantâneo, e por parte do Distribution Agent ou Merge Agent ao aplicar os arquivos de instantâneo. Em alguns casos, isso pode reduzir a velocidade da geração de instantâneos e aumentar o tempo para se aplicar um instantâneo. Além disso, instantâneos compactados não podem ser retomados no caso de uma falha de rede; consequentemente, não são apropriados para redes não confiáveis. Considere essa possibilidade cuidadosamente ao usar instantâneos compactados por uma rede.  
  
### <a name="use-sql-server-management-studio"></a>Usar o SQL Server Management Studio
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publication>** :  
  
    1.  Selecione **Colocar os arquivos nesta pasta**, depois clique em **Procurar** para ir para o diretório ou para entrar no caminho de diretório em que os arquivos de instantâneo devem estar armazenados.  
  
        > [!NOTE]  
        >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [Proteger uma pasta de instantâneo](security/secure-the-snapshot-folder.md)  
  
    2.  Desmarque **Colocar os arquivos na pasta padrão** , exceto se for necessário que os arquivos de instantâneo sejam gravados em ambos os locais.  
  
        > [!NOTE]  
        >  Se essa caixa de seleção estiver marcada, os arquivos armazenados na pasta padrão não serão compactados. Arquivos compactados só podem ser armazenados no local alternativo especificado na etapa anterior.  
  
2.  Selecione **Compactar arquivos de instantâneo nesta pasta**.    
3.  Selecione **OK**.   

### <a name="use-transact-sql"></a>Usar o Transact-SQL

Ao [Configurar Propriedades de Instantâneo](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md), especifique o valor **compress_snapshot** como **True**. 

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>Executar scripts antes e depois da aplicação do instantâneo
É possível especificar scripts a serem executados no Assinante antes ou depois que o instantâneo é aplicado. Scripts podem ser usados por várias razões, tais como a criação de logon e esquemas (proprietários de objeto) em cada Assinante.  
  
 Especifica-se um local de arquivo para cada script, e o Agente de Instantâneo copia os arquivos de script para a atual pasta de instantâneo a cada vez que ocorrer o processo de instantâneo. O Agente de Distribuição ou Agente de Mesclagem executa o script pré-instantâneo antes de qualquer script do objeto replicado, ao aplicar um instantâneo. O Agente de Distribuição ou o Agente de Mesclagem executa o script pós-instantâneo depois que todos os outros scripts de objeto e dados replicados tentam sido aplicados. Depois que a aplicação de instantâneo for concluída e os arquivos de script forem executados com êxito, os arquivos de script são removidos do diretório de trabalho no Assinante.  
  
 O script é executado lançando o utilitário **sqlcmd** . Antes de implantar um script, execute-o com **sqlcmd** para assegurar que a execução corra conforme esperado. Os conteúdos de scripts executados antes e depois que o instantâneo é aplicado devem ser repetíveis. Por exemplo, se você criar uma tabela em um script, você deve, em primeiro lugar, verificar sua existência e tomar as ações devidas caso ela exista. O script deve ser repetível, pois se você precisar reinicializar uma assinatura para a qual o script já foi aplicado, o script será aplicado novamente quando o novo instantâneo for aplicado durante a reinicialização.  
  
 Se você estiver compactando o arquivo de instantâneo (colocando-o em um formato de arquivo CAB [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), os scripts também são compactados e colocados no arquivo CAB. Depois que o arquivo de instantâneo compactado for transferido para o Assinante e descompactado para um diretório de trabalho no Assinante, qualquer script indicado como script de pré-instantâneo será executado. Da mesma forma, qualquer script de pós-instantâneo é descompactado e executado no Assinante como última etapa aplicando-se o instantâneo.  

### <a name="execute-a-script"></a>Executar um script 

1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publication>** :    
    -   Para especificar um script a ser executado antes de o instantâneo ser aplicado, clique em **Procurar** para navegar até o script ou insira um caminho para o script na caixa de texto **Antes de aplicar o instantâneo, executar este script** .  
  
        > [!NOTE]  
        >  O Agente de Distribuição ou Agente de Mesclagem devem ter permissões de leitura para o diretório especificado. Se forem usadas assinaturas pull, você deverá especificar um diretório compartilhado como um caminho UNC, como \\\computername\scripts\myscript.sql.  
  
    -   Para especificar um script a ser executado depois de o instantâneo ser aplicado, clique em **Procurar** para navegar até o script ou insira um caminho UNC para o script na caixa de texto **Após aplicar o instantâneo, executar este script** .   
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  


## <a name="see-also"></a>Consulte Também  
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Transferir instantâneos por FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)   
 [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)     
  
  
