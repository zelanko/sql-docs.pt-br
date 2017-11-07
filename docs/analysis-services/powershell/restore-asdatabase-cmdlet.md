---
title: Cmdlet Restore-ASDatabase | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 8ab7a2d0-679c-40e6-b9b9-042184b2dfc9
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 96e61c207316b216a1706834188a4f6f235cb52e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="restore-asdatabase-cmdlet"></a>Cmdlet Restore-ASDatabase

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Restaura um arquivo de backup (.abf) do banco de dados Multidimensional ou Tabular para uma instância do Analysis Services.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Restore-ASDatabase [-RestoreFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] Locations <Microsoft.AnalysisServices.RestoreLocation[]>] [-Security <Microsoft.AnalysisServices.RestoreSecurity>] [-Password <System.SecureString>] [-StorageLocation <System.string>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Permite que um administrador de sistemas do Analysis Services restaure um banco de dados multidimensional ou tabular de um arquivo de backup (.abf) para uma instância de servidor local ou remoto. Se o arquivo que você estiver restaurando estiver criptografado, use –FilePassword para fornecer a senha que é usada para descriptografar o arquivo.  
  
 Esse cmdlet oferece suporte ao parâmetro –Credential, que pode ser usado se você configurar a instância do Analysis Services para acesso HTTP. O parâmetro –Credential usa o objeto PSCredential que fornece uma identidade de usuário do Windows. O IIS representará esse usuário ao conectar-se ao Analysis Services. A identidade deve ter permissões de administrador de sistema na instância do Analysis Services para restaurar o arquivo.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-restorefile-string"></a>-RestoreFile \<cadeia de caracteres >  
 Especifica o caminho e o nome do arquivo a ser restaurado. Se você especificar apenas o nome do arquivo, sem o caminho, o local de backup padrão será assumido.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-name-string"></a>-Nome \<cadeia de caracteres >  
 Especifica o banco de dados do Analysis Services a ser restaurado.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 Substitui um banco de dados que usa o mesmo nome e local.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-locations-microsoftanalysisservicesrestorelocation"></a>-Locais \<[Microsoft.AnalysisServices.RestoreLocation] >  
 Especifica o local remoto das partições remotas a serem restauradas.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-security-microsoftanalysisservicesrestoresecurity"></a>-Segurança \<Microsoft.AnalysisServices.RestoreSecurity >  
 Representa as configurações de segurança usadas na operação de restauração. Os valores válidos são CopyAll, SkipMembership, IgnoreSecurity. CopyAll restaura funções e membros. SkipMembership apenas recria a função. IgnoreSecurity restaura o banco de dados, sem funções.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-password-securestring"></a>-Senha \<SecureString >  
 Especifica uma senha a ser usada para restaurar um arquivo de backup criptografado. Você deve especificar a senha que foi usada originalmente para criptografar o arquivo.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-storagelocation-string"></a>-StorageLocation \<cadeia de caracteres >  
 Especifica o local de armazenamento do banco de dados. Este é o local dos arquivos de banco de dados no sistema de arquivos. Defina este parâmetro se você não estiver usando o local padrão, que é a pasta de backup da instância de destino.  
  
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
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer e -OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|System.string<br /><br /> Você pode inserir os valores da cadeia de caracteres no cmdlet.|  
|Saídas|Nenhum.|  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase awtest.abf testawrestoredb –security:CopyAll  
```  
  
 Este comando restaura um arquivo de backup (awtest.abf) do Analysis Services na pasta de backup local para a instância padrão do Analysis Services local. O nome do banco de dados não precisa existir; nesse caso, o nome do banco de dados é especificado como parte da operação de restauração. Adicionar –Security:CopyAll preenche as funções e a associação de função do banco de dados de backup no novo banco de dados restaurado.  
  
## <a name="example-2"></a>Exemplo 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile testdb.abf –name AWTEST2 –password:$pwd  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 As linhas 1 e 2 são usadas para solicitar a senha usada para criptografar o arquivo.  
  
 A linha 3 restaura um arquivo de backup (testdb.abf) criptografado do Analysis Services de uma pasta de backup local de uma instância padrão do Analysis Services.  
  
 As linhas 4 e 5 removem a senha.  
  
## <a name="example-3-remote-scenario"></a>Exemplo 3 (cenário remoto)  
 Este exemplo demonstra como restaurar um arquivo de backup local de um compartilhamento de arquivos para uma instância remota do Analysis Services. Neste exemplo, um arquivo de backup é restaurado como um banco de dados denominado **internetsales** em uma instância padrão do Analysis Services em um computador chamado **ssas-aw-srv01**.  
  
 O arquivo de backup está localizado em um compartilhamento de rede, com acesso de leitura público. A instância remota do Analysis Services deve ter permissão de leitura para o arquivo. O local do arquivo deve ser um compartilhamento de rede (nenhuma unidade).  
  
 Observe que neste exemplo não conta com o provedor SQLAS. Você pode executar o cmdlet como um comando autônomo.  
  
```  
PS SQLSERVER:\> restore-asdatabase -restorefile "\\FileServer01\DBFiles\InternetSalesTabular.abf" -name "internetsales  
" -server "SSAS-AW-SRV01"  
```  
  
## <a name="example-4"></a>Exemplo 4  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile “\\myremoteserver\backups\testdb.abf” –name Contoso_Retail –server myremoteserver –storagelocation “\\myremoteserver\restoreDBFiles”  
```  
  
 Este comando restaura um arquivo de backup (testdb.abf) criptografado do Analysis Services em uma pasta de backup remota de uma instância padrão remota do Analysis Services. O parâmetro –StorageLocation é usado para colocar os arquivos de banco de dados em um local não padrão. Neste caso, um arquivo compartilhado denominado restoreDBfiles.  
  

