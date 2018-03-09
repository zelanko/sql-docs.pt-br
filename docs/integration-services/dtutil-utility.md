---
title: "Utilitário dtutil | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- verifying packages
- checking packages
- moving packages
- packages [Integration Services], command line options
- command prompt [Integration Services]
- SQL Server Integration Services packages, command line options
- copying packages
- existence testing [Integration Services]
- Integration Services packages, command line options
- SSIS packages, command line options
- deleting packages
- dtutil utility
- removing packages
- relocating packages
ms.assetid: 6c7975ff-acec-4e6e-82e5-a641e3a98afe
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5fcb9ddbd493f259341026d07a1867add85169e1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="dtutil-utility"></a>utilitário dtutil
  O utilitário de prompt de comando **dtutil** é usado para gerenciar pacotes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . O utilitário pode copiar, mover, excluir ou verificar a existência de um pacote. Essas ações podem ser desenvolvidas em qualquer pacote do [!INCLUDE[ssIS](../includes/ssis-md.md)] que esteja armazenado em um dos três locais: um banco de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , o Armazenamento de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] e o sistema de arquivos. Se o utilitário acessar um pacote armazenado em **msdb**, o prompt de comando poderá exigir um nome de usuário e uma senha. Se a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usar Autenticação de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , o prompt de comando solicitará um nome de usuário e uma senha. Se o nome de usuário estiver ausente, o **dtutil** tentará fazer logon no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a Autenticação do Windows. O tipo de armazenamento do pacote é identificado pelas opções **/SQL**, **/FILE**e **/DTS** .  
  
 O utilitário do prompt de comando **dtutil** não aceita o uso de arquivos de comando ou redirecionamento.  
  
 O utilitário do prompt de comando **dtutil** inclui os seguintes recursos:  
  
-   Comentários no prompt de comando, que tornam a ação do prompt de comando autodocumentada e mais fácil de compreender.  
  
-   Proteção contra substituição, para solicitar uma confirmação antes de substituir um pacote existente quando você estiver copiando ou movendo pacotes.  
  
-   Ajuda de console, para fornecer informações sobre as opções de comando para **dtutil**.  
  
> [!NOTE]  
>  Muitas das operações executadas pelo dtutil também podem ser executadas visualmente no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] quando você está conectado a uma instância do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para obter mais informações, consulte [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](../integration-services/service/package-management-ssis-service.md).  
  
 As opções podem ser digitadas em qualquer ordem. O caractere de pipe ("|") é o operador **OR** e é usado para mostrar possíveis valores. Você deve usar uma das opções delimitadas pelo pipe **OR** .  
  
 Todas as opções devem iniciar com uma barra (/) ou um sinal de menos (-). Porém, não inclua um espaço em branco entre a barra ou o sinal de menos e o texto da opção. Se isso for feito, ocorrerá uma falha no comando.  
  
 Os argumentos devem ser cadeias de caracteres que sejam colocadas entre aspas ou que não contenham espaços em branco.  
  
 Aspas duplas dentro de cadeias de caracteres que são colocadas entre aspas representam aspas simples.  
  
 Opções e argumentos, excetos em senhas, não diferenciam maiúsculas e minúsculas.  
  
 **Considerações sobre a instalação em computadores de 64 bits**  
  
 Em um computador de 64 bits, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] instala a versão de 64 bits dos utilitários **dtexec** (dtexec.exe) e **dtutil** (dtutil.exe). Para instalar versões de 32 bits dessas ferramentas do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , você deve selecionar Ferramentas de Cliente ou [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] durante a instalação.  
  
 Por padrão, um computador de 64 bits que tem as versões de 64 e de 32 bits de um prompt de comando do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] instaladas executará a versão de 32 bits no prompt de comando. A versão de 32 bits é executada porque o caminho do diretório da versão de 32 bits aparece na variável de ambiente PATH antes do caminho do diretório da versão de 64 bits. (Normalmente, o caminho do diretório de 32 bits é *\<drive>*:\Program Files(x86)\Microsoft SQL Server\130\DTS\Binn, enquanto o caminho do diretório de 64 bits é *\<drive>*:\Program Files\Microsoft SQL Server\130\DTS\Binn.)  
  
> [!NOTE]  
>  Se você usar o SQL Server Agent para executar o utilitário, o SQL Server Agent usará automaticamente a versão de 64 bits do utilitário. O SQL Server Agent usa o Registro, não a variável de ambiente PATH, para localizar o executável correto do utilitário.  
  
 Para garantir que a versão de 64 bits do utilitário no prompt de comando seja executada, execute uma das seguintes ações:  
  
-   Abra uma janela do Prompt de Comando, altere para o diretório que contém a versão de 64 bits do utilitário *(\<drive>*:\Program Files\Microsoft SQL Server\130\DTS\Binn) e execute o utilitário nesse local.  
  
-   No prompt de comando, execute o utilitário inserindo o caminho completo (*\<drive>*:\Program Files\Microsoft SQL Server\130\DTS\Binn) para a versão de 64 bits do utilitário.  
  
-   Altere permanentemente a ordem dos caminhos na variável de ambiente PATH colocando o caminho de 64 bits (*\<drive>*:\Program Files\Microsoft SQL Server\130\DTS\Binn) antes do caminho de 32 bits (*\<drive>*:\ Program Files(x86)\Microsoft SQL Server\130\DTS\Binn) na variável.  
  
## <a name="syntax"></a>Sintaxe  
  
```dos
dtutil /option [value] [/option [value]]...  
```  
  
#### <a name="parameters"></a>Parâmetros  
  
|Opção|Description|  
|------------|-----------------|  
|/?|Exibe as opções do prompt de comando.|  
|/C[opy] *location;destinationPathandPackageName*|Especifica uma ação de cópia em um pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] . O uso desse parâmetro requer que você especifique primeiro o local do pacote usando a opção **/FI**, **/SQ**ou **/DT** . Em seguida, especifique o nome de pacote do destino local. O argumento *destinationPathandPackageName* especifica onde o pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] é copiado. Se o *location* de destino for **SQL**, os argumentos *DestUser*, *DestPassword* e *DestServer* também deverão ser especificados no comando.<br /><br /> Quando a ação **Copy** encontra um pacote existente no destino, o **dtutil** solicita que o usuário confirme a exclusão do pacote. A resposta **Y** substitui o pacote e **N** encerra o programa. Quando o comando inclui o argumento *Quiet* , nenhum prompt aparece e todos os pacotes existentes são substituídos.|  
|/Dec[rypt] *password*|(Opcional). Define a senha de decodificação usada ao carregar um pacote com criptografia de senha.|  
|/Del[ete]|Exclui o pacote especificado pelo *SQL*, *DTS* ou pela opção *FILE* . Se **dtutil** não puder excluir o pacote, o programa será encerrado.|  
|/DestP[assword] *password*|Especifica a senha usada com a opção SQL para estabelecer conexão com uma instância de destino do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Ocorrerá um erro caso *DESTPASSWORD* seja especificado em uma linha de comando que não inclui a opção *DTSUSER* .<br /><br /> Observação: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)].|  
|/DestS[erver] *server_instance*|Especifica o nome do servidor usado com qualquer ação que faça com que um destino seja salvo no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. É usado para identificar um servidor não local ou não padrão ao salvar um pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] . É um erro especificar *DESTSERVER* em uma linha de comando que não tem uma ação associada ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ações como *SIGN SQL*, *COPY SQL*ou opções *MOVE SQL* seriam comandos apropriados para a combinação com essa opção.<br /><br /> Um nome de instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode ser especificado adicionando uma barra invertida e o nome de instância ao nome do servidor.|  
|/DestU[ser] *username*|Especifica o nome de usuário usado com as opções *SIGN SQL*, *COPY SQL*e *MOVE SQL* para estabelecer conexão com uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . É um erro especificar *DESTUSER* em uma linha de comando que não inclui a opção *SIGN SQL*, *COPY SQL*ou *MOVE SQL* .|  
|/Dump *process ID*|(Opcional.) Faz com que o processo especificado, o utilitário **dtexec** ou o processo **dtsDebugHost.exe** , faça uma pausa e crie os arquivos de despejo de depuração, .mdmp e .tmp.<br /><br /> Observação: para usar a opção **/Dump**, é preciso ter direitos de usuário de Programas de Depuração (SeDebugPrivilege).<br /><br /> Para localizar o *process ID* para o processo que você deseja pausar, use o Gerenciador de Tarefas do Windows.<br /><br /> Por padrão, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] armazena os arquivos de despejo de depuração na pasta *\<unidade>*:\Arquivos de Programas\Microsoft SQL Server\130\Shared\ErrorDumps.<br /><br /> Para saber mais sobre o utilitário **dtexec** e o processo **dtsDebugHost.exe** , consulte [dtexec Utility](../integration-services/packages/dtexec-utility.md) e [Building, Deploying, and Debugging Custom Objects](../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).<br /><br /> Para obter mais informações sobre os arquivos de despejo de depuração, consulte [Generating Dump Files for Package Execution](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).<br /><br /> Observação: os arquivos de despejo de depuração podem conter informações confidenciais. Use uma ACL (lista de controle de acesso) para restringir o acesso aos arquivos ou copie os arquivos em uma pasta que tenha acesso restrito.|  
|/DT[S] *filespec*|Especifica que o pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] a ser operado está no Armazenamento de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] . O argumento *filespec* deve incluir o caminho da pasta, iniciando pela raiz do Repositório de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] . Por padrão, os nomes das pastas raiz no arquivo de configuração são "MSDB" e "File System". Os caminhos que contêm um espaço devem ser delimitados usando aspas duplas.<br /><br /> Se a opção DT[S] for especificada na mesma linha de comando como qualquer uma das opções a seguir, DTEXEC_DTEXECERROR será retornado:<br /><br /> **FILE**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/En[crypt] *{SQL &#124; FILE}; Path;ProtectionLevel[;password]*|(Opcional). Criptografa o pacote carregado com o nível de proteção e senha especificados e o salva no local especificado em *Path*. O *ProtectionLevel* determina se é obrigatório o uso de uma senha.<br /><br /> *SQL* – Caminho é o nome do pacote de destino.<br /><br /> *FILE* – Caminho é o caminho completamente qualificado e o nome de arquivo do pacote.<br /><br /> *DTS* – Não há suporte para esta opção atualmente.<br /><br /> Opções do*ProtectionLevel* :<br /><br /> Nível 0: extrai informações confidenciais.<br /><br /> Nível 1: as informações confidenciais são criptografadas usando as credenciais de usuários locais.<br /><br /> Nível 2: as informações confidenciais são criptografadas usando uma senha obrigatória.<br /><br /> Nível 3: o pacote é criptografado usando uma senha obrigatória.<br /><br /> Nível 4: o pacote é criptografado usando as credenciais de usuários locais.<br /><br /> Nível 5: o pacote usa criptografia de armazenamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|/Ex[ists]|(Opcional). Usado para determinar se existe um pacote. **dtutil** tenta localizar o pacote especificado pelas opções *SQL*, *DTS* ou *FILE* . Se **dtutil** não puder localizar o pacote especificado, DTEXEC_DTEXECERROR será retornado.|  
|/FC[reate] {*SQL* &#124; *DTS*};*ParentFolderPath;NewFolderName*|(Opcional). Crie uma nova pasta com o nome que você especificou em *NewFolderName*. O local da nova pasta é indicado pelo *ParentFolderPath*.|  
|/FDe[lete] {*SQL* &#124; *DTS*}[;*ParentFolderPath;FolderName]*|(Opcional). Exclui do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou [!INCLUDE[ssIS](../includes/ssis-md.md)] a pasta que foi especificada pelo nome em *FolderName*. O local da pasta a ser excluída é indicado pelo *ParentFolderPath*.|  
|/FDi[rectory] {*SQL* &#124; *DTS*};*FolderPath[;S]*|(Opcional). Lista os conteúdos, tanto de pastas quanto de pacotes, em uma pasta no [!INCLUDE[ssIS](../includes/ssis-md.md)] ou no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O parâmetro opcional *FolderPath* especifica a pasta da qual você deseja exibir o conteúdo. O parâmetro opcional *S* especifica que você deseja exibir uma listagem do conteúdo das subpastas da pasta especificada no *FolderPath*.|  
|/FE[xists ] {*SQL* &#124; *DTS*};*FolderPath*|(Opcional). Verifica se a pasta especificada existe no [!INCLUDE[ssIS](../includes/ssis-md.md)] ou no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O parâmetro *FolderPath* é o caminho e o nome da pasta a ser verificada.|  
|/Fi[le] *filespec*|Essa opção especifica que o pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] a ser operado está no sistema de arquivos. O valor *filespec* pode ser fornecido como caminho local ou caminho UNC (Convenção de Nomenclatura Universal).<br /><br /> Se a opção *File* for especificada na mesma linha de comando como qualquer uma das opções a seguir, DTEXEC_DTEXECERROR será retornado:<br /><br /> **DTS**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/FR[ename] {*SQL* &#124; *DTS*} [;*ParentFolderPath; OldFolderName;NewFolderName]*|(Opcional). Renomeia uma pasta no [!INCLUDE[ssIS](../includes/ssis-md.md)] ou no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. *ParentFolderPath* é o local da pasta a ser renomeada. *OldFolderName* é o nome atual da pasta e *NewFolderName* é o novo nome a ser definido para a pasta.|  
|/H[elp] *option*|Exibe texto de ajuda extenso que mostra as opções do **dtutil** e descreve seu uso. O argumento da opção é opcional. Se o argumento for incluído, o texto de Ajuda incluirá informações detalhadas sobre a opção especificada. O exemplo a seguir exibe a ajuda para todas as opções:<br /><br /> `dtutil /H`<br /><br /> Os dois exemplos a seguir mostram como usar a opção */H* para exibir a ajuda estendida para uma opção específica, a opção */Q [uiet]* , neste exemplo:<br /><br /> `dtutil /Help Quiet`<br /><br /> `dtutil /H Q`|  
|/I[DRegenerate]|Cria um novo GUID para o pacote e atualiza a propriedade ID do pacote. Quando um pacote é copiado, a ID do pacote permanece a mesma; portanto, os arquivos de log contêm o mesmo GUID para ambos os pacotes. Essa ação cria um novo GUID para o pacote copiado recentemente para distingui-lo do original.|  
|/M[ove] {*SQL* &#124; *File* &#124; *DTS*}; *pathandname*|Especifica uma ação de movimentação em um pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para usar esse parâmetro, primeiro especifique o local do pacote usando a opção **/FI**, **/SQ**ou **/DT** . Em seguida, especifique a ação **Mover** . Essa ação requer dois argumentos que são separados por um ponto-e-vírgula:<br /><br /> O argumento de destino pode especificar *SQL*, *FILE*ou *DTS*. Um destino *SQL* pode incluir as opções *DESTUSER*, *DESTPASSWORD*e *DESTSERVER* .<br /><br /> O argumento *pathandname* especifica o local do pacote: *SQL* usa o caminho e o nome do pacote, *FILE* usa um caminho UNC ou local e *DTS* usa um local que está relacionado à raiz do Repositório de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] . Quando o destino for *FILE* ou *DTS*, o argumento de caminho não inclui o nome de arquivo. Em vez disso, ele usa o nome do pacote no local especificado como o nome de arquivo.<br /><br /> <br /><br /> Quando a ação **MOVER** encontra um pacote existente no destino, o **dtutil** solicita que você confirme a substituição do pacote. A resposta **Y** substitui o pacote e **N** encerra o programa. Quando o comando inclui a opção *QUIET* , nenhum prompt aparece e todos os pacotes existentes são substituídos.|  
|/Q[uiet]|Para as solicitações de confirmação que podem aparecer quando um comando que inclui a opção **COPY**, **MOVE**ou **SIGN** é executado. Essas solicitações aparecem se um pacote com o mesmo nome do pacote especificado já existir no computador de destino ou se o pacote especificado já estiver assinado.|  
|/R[emark] *text*|Adiciona um comentário à linha de comando. O argumento de comentário é opcional. Se o texto de comentário incluir espaços, ele deverá ser colocado entre aspas. Você pode incluir várias opções REM em uma linha de comando.|  
|/Si[gn] {*SQL* &#124; *File* &#124; *DTS*}; *path*; *hash*|Assina um pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] . Essa ação usa três argumentos necessários que são separados por ponto-e-vírgula; destination, path e hash:<br /><br /> O argumento de destino pode especificar *SQL*, *FILE*ou *DTS*. Um destino SQL pode incluir as opções *DESTUSER*, *DESTPASSWORD* e *DESTSERVER* .<br /><br /> O argumento de caminho especifica o local do pacote para aplicar a ação.<br /><br /> O argumento de hash especifica um identificador de certificado expresso como uma cadeia de caracteres hexadecimal de comprimento variado.<br /><br /> Para obter mais informações, consulte [Identificar a origem de pacotes com assinaturas digitais](../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).<br /><br /> <br /><br /> **\*\* Importante \*\*** Quando configurado para verificar a assinatura do pacote, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] apenas verifica se a assinatura digital está presente, se é válida e se provém de uma origem confiável. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]*não* verifica se o pacote foi alterado.|  
|/SourceP[assword] *password*|Especifica a senha usada com as opções *SQL* e *SOURCEUSER* para ativar a recuperação de um pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] armazenado em um banco de dados em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . É um erro especificar *SOURCEPASSWORD* em uma linha de comando que não inclui a opção **SOURCEUSER** .<br /><br /> Observação: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SourceS[erver] *server_instance*|Especifica o nome do servidor usado com a opção **SQL** para ativar a recuperação de um pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] armazenado no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. É um erro especificar *SOURCESERVER* em uma linha de comando que não inclui a opção *SIGN SQL*, *COPY* *SQL*ou *MOVE* *SQL* .<br /><br /> Um nome de instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode ser especificado adicionando uma barra invertida e o nome de instância ao nome do servidor.|  
|/SourceU[ser] *username*|Especifica o nome de usuário usado com as opções *SOURCESERVER* para ativar a recuperação de um pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] armazenado no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . É um erro especificar *SOURCEUSER* em uma linha de comando que não inclui a opção *SIGN SQL*, *COPY SQL*ou *MOVE SQL* .<br /><br /> Observação: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SQ[L] *package_path*|Especifica o local de um pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] . Essa opção indica que o pacote está armazenado no banco de dados **msdb** . O argumento *package_path* especifica o caminho e nome do pacote [!INCLUDE[ssIS](../includes/ssis-md.md)] . Os nomes de pasta são finalizados com barras invertidas.<br /><br /> Se a opção *SQL* for especificada na mesma linha de comando como qualquer uma das opções a seguir, DTEXEC_DTEXECERROR será retornado:<br /><br /> *DTS*<br /><br /> *FILE*<br /><br /> A opção *SQL* pode ser acompanhada por zero ou uma instância das seguintes opções:<br /><br /> *SOURCEUSER*<br /><br /> *SOURCEPASSWORD*<br /><br /> *SOURCESERVER*<br /><br /> <br /><br /> Se *SOURCEUSERNAME* não for incluído, a Autenticação do Windows será usada para acessar o pacote. *SOURCEPASSWORD* é permitido somente se *SOURCEUSER* estiver presente. Se *SOURCEPASSWORD* não for incluído, será usada uma senha em branco.<br /><br /> **\*\* Importante \*\*** [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]|  
  
## <a name="dtutil-exit-codes"></a>Códigos de saída do dtutil  
 O utilitário**dtutil** define um código de saída que alerta quando forem detectados erros de sintaxe, quando forem usados argumentos incorretos ou quando forem especificadas combinações de opções inválidas. Caso contrário, o utilitário indicará "A operação foi concluída com êxito". A tabela a seguir lista os valores que o utilitário **dtutil** pode definir ao sair.  
  
|Valor|Description|  
|-----------|-----------------|  
|0|O utilitário foi executado com êxito.|  
|1|O utilitário falhou.|  
|4|O utilitário não pode localizar o pacote solicitado.|  
|5|O utilitário não pode carregar o pacote solicitado.|  
|6|O utilitário não pode resolver a linha de comando porque contém erros sintáticos ou semânticos.|  
  
## <a name="remarks"></a>Remarks  
 Você não pode usar arquivos de comandos ou redirecionamento com **dtutil**.  
  
 A ordem das opções dentro da linha de comando não é significativa.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir detalham cenários comuns do uso da linha de comando.  
  
### <a name="copy-examples"></a>Exemplos de cópia  
 Para copiar um pacote armazenado no banco de dados **msdb** em uma instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a Autenticação do Windows para o Armazenamento de Pacotes do SSIS, use a seguinte sintaxe:  
  
```dos
dtutil /SQL srcPackage /COPY DTS;destFolder\destPackage   
```  
  
 Para copiar um pacote de um local para outro no sistema de arquivos e fornecer à cópia outro nome, use a seguinte sintaxe:  
  
```dos
dtutil /FILE c:\myPackages\mypackage.dtsx /COPY FILE;c:\myTestPackages\mynewpackage.dtsx  
```  
  
 Para copiar um pacote em um sistema de arquivos local para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] hospedado em outro computador, use a seguinte sintaxe:  
  
```dos
dtutil /FILE c:\sourcepkg.dtsx /DestServer <servername> /COPY SQL;destpkgname  
```  
  
 Como as opções */DestU[ser]* e */DestP[assword]* não foram usadas, a Autenticação de Windows é assumida.  
  
 Para criar uma nova ID a um pacote depois que ele for copiado, use a seguinte sintaxe:  
  
```dos
dtutil /I /FILE copiedpkg.dtsx   
```  
  
 Para criar uma nova ID para todos os pacotes em uma determinada pasta, use a seguinte sintaxe:  
  
```dos
for %%f in (C:\test\SSISPackages\*.dtsx) do dtutil.exe /I /FILE %%f  
```  
  
 Use apenas um sinal de porcentagem (%) ao digitar o comando no prompt de comando. Use dois sinais de porcentagem (%%) se o comando for usado dentro de um arquivo em lotes.  
  
### <a name="delete-examples"></a>Exemplos de exclusão  
 Para excluir um pacote armazenado no banco de dados **msdb** em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do Windows, use a seguinte sintaxe:  
  
```dos
dtutil /SQL delPackage /DELETE  
```  
  
 Para excluir um pacote armazenado no banco de dados **msdb** em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , use a seguinte sintaxe:  
  
```dos
dtutil /SQL delPackage /SOURCEUSER srcUserName /SOURCEPASSWORD #8nGs*w7F /DELETE  
```  
  
> [!NOTE]  
>  Para excluir um pacote de um servidor nomeado, inclua a opção **SOURCESERVER** e seu argumento. Você só pode especificar um servidor usando a opção *SQL* .  
  
 Para excluir um pacote armazenado no Armazenamento de Pacotes SSIS, use a seguinte sintaxe:  
  
```dos
dtutil /DTS delPackage.dtsx /DELETE  
```  
  
 Para excluir um pacote armazenado no sistema de arquivos, use a seguinte sintaxe:  
  
```dos
dtutil /FILE c:\delPackage.dtsx /DELETE  
```  
  
### <a name="exists-examples"></a>Exemplos de existência  
 Para determinar se existe um pacote no banco de dados **msdb** em uma instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do Windows, use a seguinte sintaxe:  
  
```dos
dtutil /SQL srcPackage /EXISTS  
```  
  
 Para determinar se existe um pacote no banco de dados **msdb** em uma instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , use a seguinte sintaxe:  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD *hY$d56b /EXISTS  
```  
  
> [!NOTE]  
>  Para determinar se existe um pacote em um servidor nomeado, inclua a opção **SOURCESERVER** e seu argumento. Você só pode especificar um servidor usando a opção SQL.  
  
 Para determinar se existe um pacote no armazenamento de pacotes local, use a seguinte sintaxe:  
  
```dos
dtutil /DTS srcPackage.dtsx /EXISTS  
```  
  
 Para determinar se existe um pacote no sistema de arquivos local, use a seguinte sintaxe:  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /EXISTS  
```  
  
### <a name="move-examples"></a>Exemplos de movimentação  
 Para mover um pacote armazenado no Repositório de Pacotes SSIS do banco de dados **msdb** em uma instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do Windows, use a seguinte sintaxe:  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE SQL;destPackage  
```  
  
 Para mover um pacote armazenado no banco de dados **msdb** em uma instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para o banco de dados **msdb** em outra instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , use a seguinte sintaxe:  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD $Hj45jhd@X /MOVE SQL;destPackage /DESTUSER destUserName /DESTPASSWORD !38dsFH@v  
```  
  
> [!NOTE]  
>  Para mover um pacote de um servidor nomeado para outro, inclua as opções **SOURCES** e **DESTS** e seus argumentos. Você só pode especificar os servidores usando a opção *SQL* .  
  
 Para mover um pacote armazenado no Armazenamento de Pacotes SSIS, use a seguinte sintaxe:  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE DTS;destPackage.dtsx  
```  
  
 Para mover um pacote armazenado no sistema de arquivos, use a seguinte sintaxe:  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /MOVE FILE;c:\destPackage.dtsx  
```  
  
### <a name="sign-examples"></a>Exemplos de assinatura  
 Para assinar um pacote armazenado em um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em uma instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa a Autenticação do Windows, use a seguinte sintaxe:  
  
```dos
dtutil /FILE srcPackage.dtsx /SIGN FILE;destpkg.dtsx;1767832648918a9d989fdac9819873a91f919  
```  
  
 Para localizar informações sobre seu certificado, use **CertMgr**. O código hash pode ser exibido no utilitário **CertMgr** selecionando o certificado e clicando em **Exibir** para exibir as propriedades. A guia **Detalhes** fornece mais informações sobre o certificado. A propriedade **Thumbprint** é usada como o valor de hash, com espaços removidos.  
  
> [!NOTE]  
>  O hash usado neste exemplo não é um hash real.  
  
 Para obter mais informações, consulte a seção CertMgr em [Assinando e verificando o código de verificação com Authenticode](http://go.microsoft.com/fwlink/?LinkId=78100).  
  
### <a name="encrypt-examples"></a>Exemplos de criptografia  
 O exemplo a seguir criptografa o arquivo PackageToEncrypt.dtsx para o arquivo EncryptedPackage.dts usando criptografia completa de pacote, com uma senha. A senha usada para a criptografia é *EncPswd*.  
  
```dos
dtutil /FILE PackageToEncrypt.dtsx /ENCRYPT file;EncryptedPackage.dtsx;3;EncPswd  
```  
  
## <a name="see-also"></a>Consulte Também  
[Executar pacotes do SSIS (Integration Services)](../integration-services/packages/run-integration-services-ssis-packages.md)  
  
  
