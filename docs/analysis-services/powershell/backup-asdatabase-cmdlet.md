---
title: Cmdlet backup-ASDatabase | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3fabe81584debdafa73f04c1915a00f947dacad6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="backup-asdatabase-cmdlet"></a>Cmdlet Backup-ASDatabase
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Fazer backup de um banco de dados multidimensional ou tabular do Analysis Services para um arquivo de backup (.abf) do Analysis Services.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Backup-ASDatabase [-BackupFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
 `Backup-ASDatabase –Database <Microsoft.AnalysisServices.Database> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Permite que um administrador de sistemas do Analysis Services faça backup de um banco de dados multidimensional ou tabular para um arquivo de backup. Se você não especificar um local, será usado o local do backup padrão que foi especificado durante a instalação.  
  
 Os arquivos de que você faz backup podem ser criptografados. Use –FilePassword para criptografar o arquivo. Para restaurar o arquivo mais tarde, é preciso fornecer a mesma senha especificada para descriptografá-lo.  
  
 Esse cmdlet oferece suporte ao parâmetro –Credential, que pode ser usado se você configurar a instância do Analysis Services para acesso HTTP. O parâmetro –Credential usa o objeto PSCredential que fornece uma identidade de usuário do Windows. O IIS representará esse usuário ao conectar-se ao Analysis Services. A identidade deve ter permissões de administrador de sistema na instância do Analysis Services para executar o backup.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-backupfile-string"></a>-BackupFile \<cadeia de caracteres >  
 Especifica o caminho e o nome do arquivo de backup. Se você especificar apenas o nome do arquivo, sem o caminho, que o local de backup padrão será usado. Este parâmetro só será usado com o parâmetro –Name.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-name-string"></a>-Nome \<cadeia de caracteres >  
 Especifica o banco de dados do Analysis Services do qual fazer backup. Você poderá especificar um banco de dados usando o parâmetro –Database ou o parâmetro –Name se desejar passar o nome como uma cadeia de caracteres.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 Substitui um arquivo de backup do mesmo nome.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-backupremotepartitions-switchparameter"></a>-BackupRemotePartitions \<SwitchParameter >  
 Especifica se as partições remotas serão incluídas no backup.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-applycompressionswitchparameter"></a>-ApplyCompression\<SwitchParameter >  
 Especifica se deseja compactar o arquivo de backup.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-filepassword-securestring"></a>-FilePassword \<SecureString >  
 Especifica uma senha a ser usada com a criptografia de arquivo de backup.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-locations-microsoftanalysisservicesbackuplocation"></a>-Locais \<[Microsoft.AnalysisServices.BackupLocation] >  
 Especifica o local em que o arquivo de backup será armazenado.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-server-string"></a>-Servidor \<cadeia de caracteres >  
 Especifica a instância do Analysis Services que o cmdlet conectará e executará. Se nenhum nome de servidor for fornecido, uma conexão será feita com o localhost. Para instâncias padrão, especifique apenas o nome do servidor. Para instâncias nomeadas, use o formato nome_do_servidor\nome_da_instância. Para conexões HTTP, use o formato http[s]://servidor[:porta]/diretório_virtual/msmdpump.dll.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|localhost|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 Especifica um objeto –Credential que fornece um nome de usuário e senha do Windows. Especifique esse parâmetro somente se a instância do Analysis Services estiver configurada para acesso HTTP, usando a autenticação básica. Para conexões nativas que usam a segurança integrada, esse parâmetro é ignorado.  
  
 Se esse parâmetro estiver presente, as credenciais que ele fornece serão anexadas à cadeia de conexão. O IIS representará essa identidade de usuário ao conectar-se ao Analysis Services. Se nenhuma credencial for especificada, será usada a conta do Windows padrão do usuário que está executando a ferramenta.  
  
 Para usar este parâmetro, primeiro crie um objeto PSCredential usando Get-Credential para especificar o nome de usuário e a senha (por exemplo, `$Cred=Get-Credential “adventure-works\admin”`. Você pode redirecionar este objeto para o parâmetro –Credential `(-Credential:$Cred`).  
  
Para obter mais informações sobre o acesso HTTP, consulte [Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|True (ByValue)|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-database-microsoftanalysisservicesdatabase"></a>-Banco de dados \<[Microsoft.AnalysisServices.Database] >  
 Especifica um objeto de banco de dados do Analysis Services do qual fazer backup. Você pode especificar um banco de dados usando os parâmetros -Database ou –Name. Use –Database se você desejar transportar o nome do banco de dados.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer e -OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Microsoft.AnalysisServices.Database<br /><br /> Você pode transportar bancos de dados para os quais você quer fazer backup, por exemplo todos os bancos de dados de uma instância específica.|  
|Saídas|Nenhuma.|  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >backup-asdatabase awdb-20110930.abf “Adventure Works” -AllowOverwrite -ApplyCompression  
```  
  
 Este comando faz backup do banco de dados Adventure Works para um arquivo .abf no local padrão do backup. Se um arquivo de mesmo nome existir no local, ele será substituído.  
  
## <a name="example-2"></a>Exemplo 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >$AWDB = get-item “databases\Adventure Works”   
PS SQLSERVER:\SQLAS\Localhost\default >Backup-asdatabase –database:$AWDB –AllowOverwrite  
```  
  
 Este comando usa –Database em vez de –Backupfile e –Name. Use o parâmetro –Database se você quiser transportar o nome do banco de dados para o cmdlet.  
  
## <a name="example-3"></a>Exemplo 3  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default\databases >dir * | backup-asdatabase  
```  
  
 Este comando faz backup de todos os bancos de dados no servidor local.  
  
## <a name="example-4"></a>Exemplo 4  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\Localhost\default > backup-asdatabase –backupfile test.abf –name contoso_retail –filepassword:$pwd server myremoteserver  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 As linhas 1 e 2 são usadas para solicitar uma senha que será usada para criptografar o arquivo.  
  
 A Linha 3 faz backup do banco de dados de exemplo Contoso_Retail no servidor remoto do Analysis Services em um arquivo de backup do Analysis Services chamado test.abf, também localizado no servidor remoto. O arquivo é salvo na pasta de backup padrão da instância padrão.  
  
 As linhas 4 e 5 removem a senha.  
  
  
  
