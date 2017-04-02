---
title: "Utilit&#225;rio rskeymgmt (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servidores de relatório [Reporting Services], criptografia"
  - "juntando instâncias do servidor de relatório [SQL Server]"
  - "implantações em expansão de servidor de relatório [Reporting Services]"
  - "criptografia [Reporting Services]"
  - "várias instâncias de servidor de relatório"
  - "utilitários de prompt de comando [Reporting Services]"
  - "servidores de relatório [Reporting Services], implantações escaláveis"
  - "criptografia [Reporting Services]"
  - "utilitário rskeymgmt"
  - "implantações em expansão [Reporting Services]"
ms.assetid: 53f1318d-bd2d-4c08-b19f-c8b698b5b3d3
caps.latest.revision: 56
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 56
---
# Utilit&#225;rio rskeymgmt (SSRS)
  Extrai, restaura, cria e exclui a chave simétrica usada para proteger dados confidenciais de servidor de relatório contra acesso não autorizado. Esse utilitário também é usado para unir instâncias de servidor de relatório em uma implantação de expansão. Uma *implantação em expansão de servidor de relatório* se refere a várias instâncias do servidor de relatório que compartilham um único banco de dados do servidor de relatório.  
  
## Sintaxe  
  
```  
  
rskeymgmt {-?}  
{–eextract}  
{–aapply}  
{-ddeleteall}  
{–srecreatekey}  
{–rremoveinstancekey}  
{-jjoinfarm}  
{-iinstance}  
{-ffile}  
{-pencryptionpassword}  
{-mremotecomputer}  
{-ninstancenameofremotecomputer}  
{-uadministratoruseraccount}  
{-vadministratorpassword}  
{-ttrace}  
```  
  
## Argumentos  
 **-?**  
 Exibe a sintaxe de argumentos **rskeymgmt** .  
  
 **-e**  
 Extrai a chave simétrica usada para criptografar e descriptografar dados da instância do servidor de relatório, para que você possa copiá-los em um arquivo.  
  
 Esse argumento não exige um valor. Porém, você deve incluir argumentos adicionais na linha de comando para concluir a extração. Os argumentos que você deve especificar incluem **-f** e **-p**.  
  
 **-a**  
 Substitui uma chave simétrica existente por uma cópia que você fornece em uma senha de arquivo de backup protegido. Todas as instâncias da chave simétrica são atualizadas.  
  
 Esse argumento não exige um valor. Porém, você deve incluir argumentos adicionais na linha de comando para selecionar o arquivo que contém a chave a ser aplicada. Os argumentos que você pode especificar incluem **-f** e **-p**.  
  
 **-d**  
 Exclui todas as instâncias de chave simétrica e todos os dados criptografados em um banco de dados do servidor de relatório. Esse argumento não exige um valor.  
  
 **-s**  
 Gera uma chave simétrica nova e criptografa novamente todo o conteúdo criptografado usando a nova chave. Todas as instâncias da chave simétrica são regeneradas.  
  
 **-j**  
 Configura uma instância de servidor de relatório remota para compartilhar o banco de dados do servidor de relatório usado pela instância do servidor de relatório local.  
  
 **-r**  *installationID*  
 Remove as informações de chave simétrica de uma instância de servidor de relatório específica, removendo assim o servidor do relatório de uma implantação em expansão. O *ID_instalação* é um valor GUID que pode ser localizado no arquivo RSReportserver.config.  
  
 **-f**  *file*  
 Especifica um caminho totalmente qualificado ao arquivo que armazena uma cópia de backup das chaves simétricas.  
  
 Para **rskeymgmt -e**, a chave simétrica é gravada no arquivo especificado.  
  
 Para **rskeymgmt -a**, o valor da chave simétrica armazenado no arquivo é aplicado à instância do servidor de relatório.  
  
 **-p**  *password*  
 (Necessário para **-f**) Especifica a senha usada para fazer backup ou para aplicar uma chave simétrica. Esse valor não pode ficar em branco.  
  
 **-i**  
 Especifica uma instância do servidor de relatório local. Esse argumento será opcional se você instalou o servidor de relatório na instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o valor padrão para **-i** é MSSQLSERVER). Se você instalou o servidor de relatório como uma instância nomeada, **-i** será necessário.  
  
 **-m**  
 Especifica o nome do computador remoto que hospeda a instância do servidor de relatório que está sendo unido à implantação em expansão do servidor de relatório. Use o nome do computador que o identifica em sua rede.  
  
 **-n**  
 Especifica o nome da instância do servidor de relatório em um computador remoto. Esse argumento será opcional se você instalou o servidor de relatório na instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o valor padrão para **-n** é MSSQLSERVER). Se você instalou o servidor de relatório como uma instância nomeada, **-n** será necessário.  
  
 **-u**  *useraccount*  
 Especifica a conta de administrador no computador remoto que você está unindo à implantação em expansão. Se uma conta não for especificada, as credenciais do usuário atual serão usadas.  
  
 **-v**  *password*  
 (Necessário para **-u**) Especifica a senha de uma conta de administrador no computador remoto que você quer unir à implantação em expansão.  
  
 **-t**  *trace*  
 Produz mensagens de erro para o log de rastreamento. Esse argumento não exige um valor. Para obter mais informações, consulte [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## Permissões  
 Você deve ter permissões de administrador de sistema local para executar a ferramenta, e é necessário executá-la localmente no computador que hospeda o servidor de relatório. O utilitário rskeymgmt funciona com a instância local do Servidor de Relatório do Windows (o utilitário não pode se conectar a instâncias remotas do serviço Servidor de Relatório do Windows, portanto não pode ser usado para gerenciar chaves de criptografia em uma instância de servidor remota).  
  
> [!NOTE]  
>  Se você estiver usando os argumentos **-u** e **-v**, especifique uma conta que tenha permissões de administrador no computador remoto.  
  
## Exemplos  
 Os exemplos a seguir ilustram as maneiras de usar o **rskeymgmt**. Os exemplos a seguir mostram como extrair, restaurar e excluir chaves de criptografia e como configurar uma implantação em expansão no servidor de relatório.  
  
#### Extraindo chaves de criptografia  
 Esse exemplo mostra como criar uma cópia de backup da chave de criptografia e salvá-la em um arquivo protegido por senha em um disquete. Se o servidor de relatório for instalado como uma instância nomeada, adicione o argumento **-i**.  
  
```  
rskeymgmt -e -f a:\backupkey\keys -p <password>  
```  
  
#### Restaurando chaves de criptografia  
 Este exemplo mostra como substituir a chave de criptografia. Você deve especificar o local da cópia de backup da chave e a senha que desbloqueia o arquivo.  
  
```  
rskeymgmt -a -f a:\backupkey\keys -p <password>  
```  
  
#### Excluindo chaves de criptografia e conteúdo criptografado  
 Este exemplo mostra como excluir todas as chaves de criptografia armazenadas em um servidor de relatório. Se a sua instalação for uma implantação em expansão do servidor de relatório, as chaves de criptografia de todas as instâncias do servidor de relatório incluídas na implantação serão excluídas. A exclusão de uma chave de criptografia exclui também qualquer valor criptografado existente no banco de dados do servidor de relatório. Para obter mais informações sobre conteúdo criptografado, consulte [Armazenar dados criptografados do servidor de relatório &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/store-encrypted-report-server-data-ssrs-configuration-manager.md).  
  
```  
rskeymgmt -d  
```  
  
#### Unindo uma instância nomeada de servidor de relatório remota a uma implantação em expansão  
 Este exemplo mostra como adicionar uma instância de servidor de relatório instalada em um computador remoto a uma implantação em expansão de servidor de relatório. Você deve executar o comando em um dos computadores já configurado para usar o banco de dados compartilhado. Os argumentos de comando especificam a instância do servidor de relatório remota que você quer adicionar à implantação em expansão.  
  
```  
rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
```  
  
> [!NOTE]  
>  Uma implantação em expansão de servidor de relatório se refere a um modelo de implantação onde várias instâncias do servidor de relatório compartilham o mesmo banco de dados do servidor de relatório. Um banco de dados do servidor de relatório pode ser usado por qualquer instância que armazena suas chaves simétricas no banco de dados. Por exemplo, se um banco de dados do servidor de relatório contiver informações de chave para três instâncias do servidor de relatório, todas as três instâncias serão consideradas membros da mesma implantação em expansão.  
  
#### Unindo instâncias do servidor de relatório no mesmo computador  
 Você pode criar uma implantação em expansão para várias de instâncias do servidor de relatório instaladas no mesmo computador. Não defina os argumentos **-u** e **-v** se você estiver unindo instâncias do servidor de relatório instaladas localmente. Os argumentos **-u** e **-v** só são usados quando você estiver unindo uma instância de um computador remoto. Se você especificar os argumentos, receberá o seguinte erro: "Credenciais de usuário não podem ser usadas para conexões locais".  
  
 O exemplo a seguir ilustra a sintaxe para criar uma implantação em expansão que usa várias instâncias locais. Neste exemplo, \<**initializedinstance**> é o nome de uma instância já iniciada para usar o banco de dados do servidor de relatório e \<**newinstance**> é o nome da instância que você quer adicionar à implantação:  
  
```  
rskeymgmt -j -i <initializedinstance> -m <computer name> -n <newinstance>  
```  
  
#### Removendo chaves de criptografia para um servidor de relatório único em uma implantação em expansão  
 Este exemplo mostra como remover as chaves de criptografia para um servidor de relatório único em uma implantação em expansão de servidor de relatório. As chaves são removidas do banco de dados do servidor de relatório. Uma vez que as chaves da instância do servidor de relatório são removidas, aquela instância do servidor de relatório não poderá mais acessar dados criptografados no banco de dados, removendo-os efetivamente da implantação em expansão.  
  
 A remoção de uma instância de servidor de relatório de uma implantação em expansão exige que você especifique uma ID de instalação. A ID de instalação é um GUID armazenado no arquivo RSReportserver.config da instância do servidor de relatório para o qual você quer remover as chaves de criptografia. Você deve executar o comando a seguir no computador que você quer remover da implantação em expansão. Se o servidor de relatório estiver instalado como uma instância nomeada, use o argumento **-i** para especificar a instância. Para obter mais informações, consulte [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
```  
rskeymgmt -r <installationID>  
```  
  
## Local do arquivo  
 Rskeymgmt.exe localizado em **\<*unidade*>:\Program Files\Microsoft SQL Server\110\Tools\Binn** ou em **\<*unidade*>:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn**. Você pode executar o utilitário de qualquer pasta em seu sistema de arquivos.  
  
## Comentários  
 Um servidor de relatório criptografa credenciais armazenadas e informações de conexão. Uma chave pública e uma chave simétrica são usadas para criptografar dados. Um banco de dados do servidor de relatório deve ter chaves válidas para que o servidor de relatório seja executado. Você pode usar **rskeymgmt** para fazer backup, excluir ou restaurar as chaves. Se as chaves não puderem ser restauradas, essa ferramenta fornecerá um modo de excluir conteúdo criptografado que não pode mais ser usado.  
  
 O utilitário **rskeymgmt** é usado para gerenciar o conjunto de chaves definido durante a instalação ou durante a inicialização. Ele se conecta ao serviço Servidor de Relatório do Windows através de um ponto de extremidade RPC (Chamada de Procedimento Remoto). O serviço Servidor de Relatório do Windows deve estar em execução para que esse utilitário funcione.  
  
 Para obter mais informações sobre as chaves de criptografia, veja [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-and-manage-encryption-keys-ssrs-configuration-manager.md) e [Inicializar um servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/initialize-a-report-server-ssrs-configuration-manager.md).  
  
## Consulte também  
 [Implantação escalável: modo Nativo do Reporting Services &#40;Configuration Manager&#41;](../Topic/Scale-out%20Deployment%20%20-%20Reporting%20Services%20Native%20mode%20\(Configuration%20Manager\).md)   
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Utilitários de prompt de comando do servidor de relatório &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-and-manage-encryption-keys-ssrs-configuration-manager.md)  
  
  