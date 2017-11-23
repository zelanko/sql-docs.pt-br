---
title: Fazendo backup, restaurar e sincronizar bancos de dados (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- restoring databases [XML for Analysis]
- backing up databases [XML for Analysis]
- database backups [XML for Analysis]
- synchronization [XML for Analysis]
- database restores [XML for Analysis]
ms.assetid: 6c021b2e-6ad0-444e-b23f-4b5f72ce084b
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6d23fcaca8e9ad0d73d1e79566d2fa11348382a3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>Fazendo backup, restaurando e sincronizando bancos de dados (XMLA)
  No XML for Analysis, existem três comandos que fazem backup de bancos de dados, que os restauram e que os sincronizam:  
  
-   O [Backup](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) comando faz backup de um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados usando um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o arquivo de backup (abf), conforme descrito na seção, [fazendo backup de bancos de dados](#backing_up_databases).  
  
-   O [restaurar](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) comando restaura um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados de um arquivo. abf, conforme descrito na seção, [restaurando bancos de dados](#restoring_databases).  
  
-   O [sincronizar](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) comando sincroniza um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados com os dados e metadados de outro banco de dados, conforme descrito na seção, [sincronizando bancos de dados](#synchronizing_databases).  
  
##  <a name="backing_up_databases"></a>Fazendo backup de bancos de dados  
 Como mencionado anteriormente, o **Backup** comando faz backup de um especificado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados para um arquivo de backup. O **Backup** comando tem várias propriedades que permitem a você especifica o banco de dados de backup, o arquivo de backup a ser usado, como fazer backup de definições de segurança e as partições remotas será feito backup.  
  
> [!IMPORTANT]  
>  A conta de serviço do Analysis Services deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: função de administrador na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados do qual será feito o backup.  
  
### <a name="specifying-the-database-and-backup-file"></a>Especificando o banco de dados e o arquivo de backup  
 Para especificar o banco de dados de backup, defina o [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propriedade o **Backup** comando. O **objeto** propriedade deve conter um identificador de objeto para um banco de dados, ou ocorrerá um erro.  
  
 Para especificar o arquivo a ser criada e usada pelo processo de backup, defina o [arquivo](../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md) propriedade o **Backup** comando. O **arquivo** propriedade deve ser definida como um nome de arquivo e caminho UNC para o arquivo de backup a ser criado.  
  
 Além da especificação de que arquivo será usado para backup, defina as opções a seguir para o arquivo de backup especificado:  
  
-   Se você definir o [AllowOverwrite](../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md) propriedade como true, o **Backup** comando substitui o arquivo de backup se o arquivo especificado já existe. Se você definir o **AllowOverwrite** a propriedade como false, ocorre um erro se o arquivo de backup especificado já existe.  
  
-   Se você definir o [ApplyCompression](../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md) propriedade como true, o arquivo de backup será compactada após o arquivo é criado.  
  
-   Se você definir o [senha](../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md) propriedade como qualquer valor diferente de em branco, o arquivo de backup é criptografada usando a senha especificada.  
  
    > [!IMPORTANT]  
    >  Se **ApplyCompression** e **senha** propriedades não forem especificadas, o arquivo de backup armazena nomes de usuário e senhas contidos nas cadeias de conexão em texto não criptografado. Os dados armazenados em texto não criptografados podem ser recuperados. Para maior segurança, use o **ApplyCompression** e **senha** configurações ao compactar e criptografar o arquivo de backup.  
  
### <a name="backing-up-security-settings"></a>Fazendo backup das configurações de segurança  
 O [segurança](../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md) propriedade determina se o **Backup** comando faz backup de definições de segurança, como funções e permissões, definidas em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados. O **segurança** propriedade também determina se o arquivo de backup inclui as contas de usuário do Windows e os grupos definidos como membros das definições de segurança.  
  
 O valor de **segurança** propriedade é limitada a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*SkipMembership*|Inclua definições de segurança, mas exclua informações de associação, no arquivo de backup.|  
|*CopyAll*|Inclua definições de segurança e informações de associação no arquivo de backup.|  
|*IgnoreSecurity*|Exclua definições de segurança do arquivo de backup.|  
  
### <a name="backing-up-remote-partitions"></a>Fazendo backup de partições remotas  
 Para fazer backup de partições remotas no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados, defina o [BackupRemotePartitions](../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md) propriedade o **Backup** comando como true. Essa configuração faz com que o **Backup** comando para criar um arquivo de backup remoto para cada fonte de dados remota que é usado para armazenar partições remotas para o banco de dados.  
  
 Para cada fonte de dados remotos fazer backup, você pode especificar o arquivo de backup correspondente, incluindo um [local](../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) elemento o [locais](../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md) propriedade o **Backup** comando. O **local** elemento deve ter seu **arquivo** propriedade definida como o nome de arquivo e caminho UNC do arquivo de backup remoto e sua [DataSourceID](../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md) propriedade definida como o identificador do a fonte de dados remota definida no banco de dados.  
  
##  <a name="restoring_databases"></a>Restaurando bancos de dados  
 O **restaurar** comando restaura um especificado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados de um arquivo de backup. O **restaurar** comando tem várias propriedades que permitem a você especifica o banco de dados para restaurar o arquivo de backup a ser usado, como restaurar definições de segurança, as partições remotas a serem armazenados e a realocação OLAP relacional (ROLAP) objetos.  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de restauração deve ter permissão para ler no local de backup especificado para cada arquivo. Para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que não esteja instalado no servidor, o usuário também deve ser membro da função de servidor dessa instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para substituir um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o usuário deve ter uma das seguintes funções: membro da função de servidor da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados a ser restaurado.  
  
> [!NOTE]  
>  Após restaurar um banco de dados existente, o usuário que o restaurou poderá perder o acesso ao banco de dados restaurado. Essa perda de acesso pode ocorrer se, no momento da execução do backup, o usuário não for membro da função de servidor, nem membro da função de banco de dados com permissões de Controle total (Administrador).  
  
### <a name="specifying-the-database-and-backup-file"></a>Especificando o banco de dados e o arquivo de backup  
 O **DatabaseName** propriedade o **restaurar** comando deve conter um identificador de objeto para um banco de dados, ou ocorrerá um erro. Se o banco de dados especificado já existir, o **AllowOverwrite** propriedade determina se o banco de dados existente será substituído. Se o **AllowOverwrite** propriedade estiver definida como false e o banco de dados especificado já existe, ocorrerá um erro.  
  
 Você deve definir o **arquivo** propriedade o **restaurar** comando para um nome de arquivo e caminho UNC para o arquivo de backup a ser restaurado no banco de dados especificado. Você também pode definir o **senha** propriedade para o arquivo de backup especificado. Se o **senha** propriedade estiver definida como qualquer valor diferente de em branco, o arquivo de backup será criptografado com a senha especificada. Se o arquivo de backup não estiver criptografado, ou se a senha especificada não corresponder à senha usada para criptografar o arquivo de backup, ocorrerá um erro.  
  
### <a name="restoring-security-settings"></a>Restaurando configurações de segurança  
 O **segurança** propriedade determina se o **restaurar** comando restaura as definições de segurança, como funções e permissões, definidas em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados. O **segurança** propriedade também determina se o **restaurar** comando inclui as contas de usuário do Windows e os grupos definidos como membros das definições de segurança como parte do processo de restauração.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*SkipMembership*|Inclua definições de segurança, mas exclua informações de associação, no banco de dados.|  
|*CopyAll*|Inclua definições de segurança e informações de associação no banco de dados.|  
|*IgnoreSecurity*|Exclua definições de segurança do banco de dados.|  
  
### <a name="restoring-remote-partitions"></a>Restaurando partições remotas  
 Para cada arquivo de backup remoto criado durante anterior **Backup** de comando, você pode restaurar sua partição remota associada incluindo um **local** elemento o **locais**propriedade o **restaurar** comando. O [DataSourceType](../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md) propriedade para cada **local** elemento deve ser excluído ou explicitamente definido como *remoto*.  
  
 Para cada uma especificada **local** elemento, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância entra em contato com a fonte de dados remota especificada no **DataSourceID** propriedade para restaurar as partições definidas no arquivo de backup remoto especificado no **arquivo** propriedade. Além de **DataSourceID** e **arquivo** propriedades, as propriedades a seguir estão disponíveis para cada **local** elemento usado para restaurar uma partição remota:  
  
-   Para substituir a cadeia de conexão para a fonte de dados remota especificada na **DataSourceID**, você pode definir o **ConnectionString** propriedade o **local** elemento para um cadeia de caracteres de conexão diferente. O **restaurar** comando, em seguida, usará a cadeia de caracteres de conexão que está contida no **ConnectionString** propriedade. Se **ConnectionString** não for especificado, o **restaurar** comando usa a cadeia de conexão armazenada no arquivo de backup para a fonte de dados remota especificada. Você pode usar o **ConnectionString** configuração para mover uma partição remota para uma instância remota diferente. No entanto, você não pode usar o **ConnectionString** configuração para restaurar uma partição remota para a mesma instância que contém o banco de dados restaurado. Em outras palavras, você não pode usar o **ConnectionString** propriedade para tornar uma partição remota em uma partição local.  
  
-   Para cada pasta original usada para armazenar as partições remotas na fonte de dados remoto, você pode especificar um [pasta](../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) elemento para indicar a nova pasta em que deseja restaurar todas as partições remotas armazenadas na pasta original. Se um **pasta** elemento não for especificado, o **restaurar** comando usa as pastas originais especificadas para as partições remotas contidas no arquivo de backup remoto.  
  
### <a name="relocating-rolap-objects"></a>Realocando objetos ROLAP  
 O **restaurar** comando não pode restaurar agregações ou dados para objetos que usam o armazenamento ROLAP porque essas informações estão armazenadas em tabelas em uma fonte de dados relacional subjacente. No entanto, os metadados para objetos ROLAP podem ser restaurados. Para restaurar os metadados para objetos ROLAP, o **restaurar** comando recria a estrutura da tabela em uma fonte de dados relacional.  
  
 Você pode usar o **local** elemento em um **restaurar** comando para realocar objetos ROLAP. Para cada **local** elemento usado para transferir uma fonte de dados, o **DataSourceType** propriedade deve ser definida explicitamente como *Local*. Você também deve definir o **ConnectionString** propriedade o **local** elemento para a cadeia de caracteres de conexão do novo local. Durante a restauração, o **restaurar** comando substituirá a cadeia de conexão da fonte de dados identificada pelo **DataSourceID** propriedade o **local** elemento com o valor da **ConnectionString** propriedade o **local** elemento.  
  
##  <a name="synchronizing_databases"></a>Sincronizar bancos de dados  
 O **sincronizar** comando sincroniza os dados e metadados de um especificado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados com outro banco de dados. O **sincronizar** comando tem várias propriedades que permitem que você especifique o banco de dados de origem, como sincronizar definições de segurança, as partições remotas a serem sincronizadas e a sincronização de objetos ROLAP.  
  
> [!NOTE]  
>  O **sincronizar** comando pode ser executado somente por administradores de servidor e banco de dados. Os bancos de dados de origem e de destino devem ter o mesmo nível de compatibilidade do banco de dados.  
  
### <a name="specifying-the-source-database"></a>Especificando o banco de dados de origem  
 O [fonte](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) propriedade o **sincronizar** comando contém duas propriedades, **ConnectionString** e **objeto**. O **ConnectionString** propriedade contém a cadeia de caracteres de conexão da instância que contém o banco de dados de origem, e o **objeto** propriedade contém o identificador de objeto para o banco de dados de origem.  
  
 O banco de dados de destino é o banco de dados atual para a sessão na qual o **sincronizar** comando seja executado.  
  
 Se o **ApplyCompression** propriedade o **sincronizar** estiver definido como true, as informações enviadas da fonte de banco de dados para o banco de dados de destino é compactado antes de serem enviados.  
  
### <a name="synchronizing-security-settings"></a>Sincronizando configurações de segurança  
 O [SynchronizeSecurity](../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md) propriedade determina se o **sincronizar** comando sincroniza as definições de segurança, como funções e permissões, definidas no banco de dados de origem. O **SynchronizeSecurity** propriedade também determina se o **sincronizar** comando inclui os grupos definidos como membros das definições de segurança e contas de usuário do Windows.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*SkipMembership*|Inclua definições de segurança, mas exclua informações de associação, no banco de dados de destino.|  
|*CopyAll*|Inclua definições de segurança e informações de associação no banco de dados de destino.|  
|*IgnoreSecurity*|Exclua definições de segurança do banco de dados de destino.|  
  
### <a name="synchronizing-remote-partitions"></a>Sincronizando partições remotas  
 Para cada fonte de dados remotos que existe no banco de dados de origem, você poderá sincronizar cada partição remota associada incluindo um **local** elemento o **locais** propriedade do  **Sincronizar** comando. Para cada **local** elemento, o **DataSourceType** propriedade deve ser excluída ou explicitamente definida como *remoto*.  
  
 Para definir e conectar-se a uma fonte de dados remotos no banco de dados de destino, o **sincronizar** comando usa a cadeia de conexão definida no **ConnectionString** propriedade o **local**  elemento. O **sincronizar** comando, em seguida, usa o **DataSourceID** propriedade o **local** elemento para identificar quais partições remotas serão sincronizadas. O **sincronizar**comando sincroniza as partições remotas na fonte de dados remota especificada no **DataSourceID** propriedade do banco de dados de origem com a fonte de dados remota especificada no  **DataSourceID** propriedade do banco de dados de destino.  
  
 Para cada pasta original usada para armazenar as partições remotas na fonte de dados remota do banco de dados de origem, você também pode especificar um **pasta** elemento o **local** elemento. O **pasta** elemento indica a nova pasta para o banco de dados de destino na qual sincronizar todas as partições remotas armazenadas na pasta original na fonte de dados remoto. Se um **pasta** elemento não for especificado, o comando Synchronize usará as pastas originais especificadas para partições remotas contidas no banco de dados de origem.  
  
### <a name="synchronizing-rolap-objects"></a>Sincronizando objetos ROLAP  
 O **sincronizar** comando não pode sincronizar agregações ou dados para objetos que usam o armazenamento ROLAP porque essas informações estão armazenadas em tabelas em uma fonte de dados relacional subjacente. No entanto, os metadados para objetos ROLAP podem ser sincronizados. Para sincronizar os metadados, o **sincronizar** comando recria a estrutura da tabela em uma fonte de dados relacional.  
  
 Você pode usar o **local** elemento em um comando Synchronize para sincronizar objetos ROLAP. Para cada **local** elemento usado para transferir uma fonte de dados, o **DataSourceType** propriedade deve ser definida explicitamente como *Local*. . Você também deve definir o **ConnectionString** propriedade o **local** elemento para a cadeia de caracteres de conexão do novo local. Durante a sincronização, o **sincronizar** comando substituirá a cadeia de conexão da fonte de dados identificada pelo **DataSourceID** propriedade o **local** elemento com o valor da **ConnectionString** propriedade o **local** elemento.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de backup &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [Restaurar o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Elemento Synchronize &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Backup e restauração de bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
