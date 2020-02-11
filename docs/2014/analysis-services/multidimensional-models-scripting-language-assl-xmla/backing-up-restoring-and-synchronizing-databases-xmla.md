---
title: Fazendo backup, restaurando e sincronizando bancos de dados (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- restoring databases [XML for Analysis]
- backing up databases [XML for Analysis]
- database backups [XML for Analysis]
- synchronization [XML for Analysis]
- database restores [XML for Analysis]
ms.assetid: 6c021b2e-6ad0-444e-b23f-4b5f72ce084b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6163a538c4e8872016f7ec572e4c177cfe92de94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702273"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>Fazendo backup, restaurando e sincronizando bancos de dados (XMLA)
  No XML for Analysis, existem três comandos que fazem backup de bancos de dados, que os restauram e que os sincronizam:  
  
-   O [comando backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) faz o backup [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de um banco [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de dados usando um arquivo de backup (. ABF), conforme descrito na seção [fazendo backup](#backing_up_databases)de banco de dados.  
  
-   O comando [Restore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) restaura um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados a partir de um arquivo. ABF, conforme descrito na seção [restaurando bancos](#restoring_databases)de dados.  
  
-   O comando [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) sincroniza um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados com os metadados de outro banco de dado, conforme descrito na seção [sincronizando bancos](#synchronizing_databases)de dados.  
  
##  <a name="backing_up_databases"></a>Fazendo backup de bancos de dados  
 Como mencionado anteriormente, o comando `Backup` faz backup de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificado em um arquivo de backup. O comando `Backup` possui diversas propriedades que permitem a você especificar o banco de dados a ser incluído no backup, o arquivo de backup a ser usado, como fazer backup de definições de segurança e as partições remotas a serem incluídas no backup.  
  
> [!IMPORTANT]  
>  A conta de serviço do Analysis Services deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: função de administrador na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados do qual será feito o backup.  
  
### <a name="specifying-the-database-and-backup-file"></a>Especificando o banco de dados e o arquivo de backup  
 Para especificar o backup do banco de dados, defina a propriedade [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) do `Backup` comando. A propriedade `Object` deve conter um identificador de objeto para um banco de dados ou ocorrerá um erro.  
  
 Para especificar o arquivo a ser criado e usado pelo processo de backup, defina a propriedade [File](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla) do `Backup` comando. A propriedade `File` dever ser definida como um caminho UNC e um nome de arquivo para o arquivo de backup a ser criado.  
  
 Além da especificação de que arquivo será usado para backup, defina as opções a seguir para o arquivo de backup especificado:  
  
-   Se você definir a propriedade [AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla) como true, o `Backup` comando substituirá o arquivo de backup se o arquivo especificado já existir. Se você definir a propriedade `AllowOverwrite` como falsa, ocorrerá um erro se o arquivo de backup especificado já existir.  
  
-   Se você definir a propriedade [ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla) como true, o arquivo de backup será compactado depois que o arquivo for criado.  
  
-   Se você definir a propriedade [senha](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla) como qualquer valor que não seja em branco, o arquivo de backup será criptografado usando a senha especificada.  
  
    > [!IMPORTANT]  
    >  Se as propriedades `ApplyCompression` e `Password` não forem especificadas, o arquivo de backup armazenará nomes de usuário e senhas contidos nas cadeias de conexão em texto não criptografado. Os dados armazenados em texto não criptografados podem ser recuperados. Para aumentar a segurança, use as configurações `ApplyCompression` e `Password` para compactar e criptografar o arquivo de backup.  
  
### <a name="backing-up-security-settings"></a>Fazendo backup das configurações de segurança  
 A propriedade de [segurança](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) determina se `Backup` o comando faz backup das definições de segurança, como funções e permissões, definidas em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] um banco de dados. A propriedade `Security` também determina se o arquivo de backup incluirá as contas de usuário do Windows e os grupos definidos como membros das definições de segurança.  
  
 O valor da propriedade `Security` está limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|*SkipMembership*|Inclua definições de segurança, mas exclua informações de associação, no arquivo de backup.|  
|*CopyAll*|Inclua definições de segurança e informações de associação no arquivo de backup.|  
|*IgnoreSecurity*|Exclua definições de segurança do arquivo de backup.|  
  
### <a name="backing-up-remote-partitions"></a>Fazendo backup de partições remotas  
 Para fazer backup de partições remotas [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no banco de dados, defina a propriedade [BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla) do `Backup` comando como true. Essa configuração faz com que o comando `Backup` crie um arquivo de backup remoto para cada fonte de dados remota usada para o armazenamento de partições remotas para o banco de dados.  
  
 Para cada fonte de dados remota de backup, você pode especificar seu arquivo de backup correspondente, incluindo um elemento [Location](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla) na propriedade [Locations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla) do `Backup` comando. O `Location` elemento deve ter sua `File` propriedade definida como o caminho UNC e o nome de arquivo do arquivo de backup remoto e sua propriedade [DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) definida como o identificador da fonte de dados remota definida no banco de dado.  
  
##  <a name="restoring_databases"></a>Restaurando bancos de dados  
 O comando `Restore` restaura um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificado de um arquivo de backup. O comando `Restore` possui diversas propriedades que permitem a você especificar o banco de dados a ser restaurado, o arquivo de backup a ser usado, como restaurar definições de segurança, as partições remotas a serem armazenadas e os objetos ROLAP.  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de restauração deve ter permissão para ler no local de backup especificado para cada arquivo. Para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que não esteja instalado no servidor, o usuário também deve ser membro da função de servidor dessa instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para substituir um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o usuário deve ter uma das seguintes funções: membro da função de servidor da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados a ser restaurado.  
  
> [!NOTE]  
>  Após restaurar um banco de dados existente, o usuário que o restaurou poderá perder o acesso ao banco de dados restaurado. Essa perda de acesso pode ocorrer se, no momento da execução do backup, o usuário não for membro da função de servidor, nem membro da função de banco de dados com permissões de Controle total (Administrador).  
  
### <a name="specifying-the-database-and-backup-file"></a>Especificando o banco de dados e o arquivo de backup  
 A propriedade `DatabaseName` do comando `Restore` deve conter um identificador de objeto para um banco de dados, ou ocorrerá um erro. Se o banco de dados especificado já existir, a propriedade `AllowOverwrite` determinará se o banco de dados existente será substituído. Se a propriedade `AllowOverwrite` for definida para como falsa e se o banco de dados especificado já existir, ocorrerá um erro.  
  
 Defina a propriedade `File` do comando `Restore` como um caminho UNC e o nome de arquivo para o arquivo de backup a ser restaurado para o banco de dados especificado. Você também pode definir a propriedade `Password` para o arquivo de backup especificado. Se a propriedade `Password` for definida como um valor diferente de em branco, o arquivo de backup será criptografado com a senha especificada. Se o arquivo de backup não estiver criptografado, ou se a senha especificada não corresponder à senha usada para criptografar o arquivo de backup, ocorrerá um erro.  
  
### <a name="restoring-security-settings"></a>Restaurando configurações de segurança  
 A propriedade `Security` determina se o comando `Restore` vai restaurar as definições de segurança, como funções e permissões, do banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A propriedade `Security` também determina se o comando `Restore` incluirá as contas de usuário e os grupos do Windows definidos como membros das definições de segurança como parte do processo de restauração.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|*SkipMembership*|Inclua definições de segurança, mas exclua informações de associação, no banco de dados.|  
|*CopyAll*|Inclua definições de segurança e informações de associação no banco de dados.|  
|*IgnoreSecurity*|Exclua definições de segurança do banco de dados.|  
  
### <a name="restoring-remote-partitions"></a>Restaurando partições remotas  
 Para cada arquivo de backup remoto criado durante o comando `Backup` anterior, você poderá restaurar sua partição remota associada incluindo um elemento `Location` na propriedade `Locations` do comando `Restore`. A propriedade [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) para cada `Location` elemento deve ser excluída ou definida explicitamente como *remota*.  
  
 Para cada elemento `Location` especificado, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] entrará em contato com a fonte de dados remota especificada na propriedade `DataSourceID` para restaurar as partições definidas no arquivo de backup remoto especificado na propriedade `File`. Além das propriedades `DataSourceID` e `File`, as propriedades a seguir estão disponíveis para cada elemento `Location` usado na restauração de uma partição remota:  
  
-   Para substituir a cadeia de conexão para uma fonte de dados remota especificada em `DataSourceID`, defina a propriedade `ConnectionString` do elemento `Location` para uma cadeia de conexão diferente. O comando `Restore` usará a cadeia de conexão contida na propriedade `ConnectionString`. Se `ConnectionString` não for especificado, o comando `Restore` usará a cadeia de conexão armazenada no arquivo de backup para a fonte de dados remota especificada. Você pode usar a configuração `ConnectionString` para mover uma partição remota para uma instância remota diferente. No entanto, não é possível usar a configuração `ConnectionString` para restaurar uma partição remota para a mesma instância que contém o banco de dados restaurado. Em outras palavras, você não poderá usar a propriedade `ConnectionString` para transformar uma partição remota em uma partição local.  
  
-   Para cada pasta original usada para armazenar as partições remotas na fonte de dados remota, você pode especificar um elemento [Folder](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla) para indicar a nova pasta na qual restaurar todas as partições remotas armazenadas na pasta original. Se um elemento `Folder` não for especificado, o comando `Restore` usará as pastas originais especificadas para as partições remotas contidas no arquivo de backup remoto.  
  
### <a name="relocating-rolap-objects"></a>Realocando objetos ROLAP  
 O comando `Restore` não pode restaurar agregações ou dados para objetos que usam o armazenamento ROLAP porque essas informações estão armazenadas em tabelas em uma fonte de dados relacional subjacente. No entanto, os metadados para objetos ROLAP podem ser restaurados. Para restaurar os metadados para objetos ROLAP, o comando `Restore` recria a estrutura de tabela em uma fonte de dados relacional.  
  
 Você pode usar o elemento `Location` em um comando `Restore` para realocar objetos ROLAP. Para cada `Location` elemento usado para realocar uma fonte de dados `DataSourceType` , a propriedade deve ser definida explicitamente como *local*. Você também precisa definir a propriedade `ConnectionString` do elemento `Location` para a cadeia de conexão do novo local. Durante a restauração, o comando `Restore` substituirá a cadeia de conexão para a fonte de dados identificada pela propriedade `DataSourceID` do elemento `Location` pelo valor da propriedade `ConnectionString` do elemento `Location`.  
  
##  <a name="synchronizing_databases"></a>Sincronizando bancos de dados  
 O comando `Synchronize` sincroniza os dados e os metadados de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificado com outro banco de dados. O comando `Synchronize` possui diversas propriedades que permitem a você especificar o banco de dados de origem, como sincronizar as definições de segurança, as partições remotas a serem sincronizadas e a sincronização de objetos ROLAP.  
  
> [!NOTE]  
>  O comando `Synchronize` pode ser executado apenas por administradores de servidor e por administradores de banco de dados. Os bancos de dados de origem e de destino devem ter o mesmo nível de compatibilidade do banco de dados.  
  
### <a name="specifying-the-source-database"></a>Especificando o banco de dados de origem  
 A propriedade [Source](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) do `Synchronize` comando contém duas propriedades, `ConnectionString` e. `Object` A propriedade `ConnectionString` armazena a cadeia de conexão da instância que contém o banco de dados de origem, e a propriedade `Object` contém o identificador de objeto para o banco de dados de origem.  
  
 O banco de dados de destino é o banco de dados atual para a sessão na qual o comando `Synchronize` é executado.  
  
 Se a propriedade `ApplyCompression` do comando `Synchronize` for definida como verdadeira, as informações enviadas do banco de dados de origem para o de destino serão compactadas antes do envio.  
  
### <a name="synchronizing-security-settings"></a>Sincronizando configurações de segurança  
 A propriedade [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) determina se o `Synchronize` comando sincroniza as definições de segurança, como funções e permissões, definidas no banco de dados de origem. A propriedade `SynchronizeSecurity` também determina se o comando `Sychronize` incluirá contas de usuário e grupos do Windows definidos como membros das definições de segurança.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|*SkipMembership*|Inclua definições de segurança, mas exclua informações de associação, no banco de dados de destino.|  
|*CopyAll*|Inclua definições de segurança e informações de associação no banco de dados de destino.|  
|*IgnoreSecurity*|Exclua definições de segurança do banco de dados de destino.|  
  
### <a name="synchronizing-remote-partitions"></a>Sincronizando partições remotas  
 Para cada fonte de dados remota existente no banco de dados de origem, você poderá sincronizar cada partição remota associada ao incluir um elemento `Location` na propriedade `Locations` do comando `Synchronize`. Para cada `Location` elemento, a `DataSourceType` propriedade deve ser excluída ou explicitamente definida como *remota*.  
  
 Para definir uma fonte de dados remota e para conectar-se a ela no banco de dados de destino, o comando `Synchronize` usará a cadeia de conexão definida na propriedade `ConnectionString` do elemento `Location`. O comando `Synchronize` usa a propriedade `DataSourceID` do elemento `Location` para identificar quais partições remotas serão sincronizadas. O `Synchronize`comando sincroniza as partições remotas na fonte de dados remota especificada na `DataSourceID` Propriedade no banco de dados de origem com a fonte de dados remota especificada `DataSourceID` na propriedade no banco de dado de destino.  
  
 Para cada pasta original usada para armazenar as partições remotas da fonte de dados remota do banco de dados de origem, também é possível especificar um elemento `Folder` no elemento `Location`. O elemento `Folder` indica a nova pasta para o banco de dados de destino no qual todas as partições remotas armazenadas na pasta original da fonte de dados remota serão sincronizadas. Se um elemento `Folder` não for especificado, o comando Synchronize usará as pastas originais especificadas para as partições remotas contidas no banco de dados de origem.  
  
### <a name="synchronizing-rolap-objects"></a>Sincronizando objetos ROLAP  
 O comando `Synchronize` não pode sincronizar agregações ou dados para objetos que usam o armazenamento ROLAP porque essas informações estão armazenadas em tabelas em uma fonte de dados relacional subjacente. No entanto, os metadados para objetos ROLAP podem ser sincronizados. Para sincronizar os metadados, o comando `Synchronize` recria a estrutura de tabela em uma fonte de dados relacional.  
  
 Você pode usar o elemento `Location` de um comando Synchronize para sincronizar objetos ROLAP. Para cada `Location` elemento usado para realocar uma fonte de dados `DataSourceType` , a propriedade deve ser definida explicitamente como *local*. . Você também precisa definir a propriedade `ConnectionString` do elemento `Location` para a cadeia de conexão do novo local. Durante a sincronização, o comando `Synchronize` substituirá a cadeia de conexão para a fonte de dados identificada pela propriedade `DataSourceID` do elemento `Location` pelo valor da propriedade `ConnectionString` do elemento `Location`.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento de backup &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Elemento Restore &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Sincronizar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Backup e restauração de bancos de dados do Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
