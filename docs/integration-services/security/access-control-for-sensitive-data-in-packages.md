---
title: Controle de acesso de dados confidenciais em pacotes | Microsoft Docs
ms.custom: security
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.packageprotectionlevel.f1
- sql13.ssis.bids.projectprotectionlevel.f1
- sql13.dts.designer.packagepassword.f1
- sql13.ssis.bids.projectpassword.f1
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services], security
- protection levels for packages [Integration Services]
- configuration files [Integration Services]
- encryption [Integration Services]
- cryptography [Integration Services]
- security [Integration Services], protection levels
ms.assetid: d4b073c4-4238-41fc-a258-4e114216e185
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9cbb736b77cef9bcb87dfa7cac2cd5a33943ca66
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79288180"
---
# <a name="access-control-for-sensitive-data-in-packages"></a>Controle de acesso de dados confidenciais em pacotes

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Para proteger os dados em um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você pode definir um nível de proteção que ajude a proteger apenas dados confidenciais ou todos os dados no pacote. Além disso, você pode criptografar esses dados com uma senha ou uma chave de usuário ou contar com o banco de dados para criptografar os dados. Além disso, o nível de proteção usado para um pacote não é necessariamente estático, mas altera todo o ciclo de vida do pacote. Defina sempre um nível de proteção durante um desenvolvimento e outro assim que implantar o pacote.  
  
> [!NOTE]  
>  Além dos níveis de proteção descritos neste tópico, você pode usar funções em nível de banco de dados fixas para proteger pacotes que são salvos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="definition-of-sensitive-information"></a>Definição de informações confidenciais  
 Em um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , as seguintes informações são definidas como *confidenciais*:  
  
-   A parte da senha de uma cadeia de caracteres de conexão. No entanto, se você selecionar uma opção que criptografa tudo, a cadeia de caracteres de conexão inteira será considerada confidencial.  
  
-   Os nós XML gerados por tarefa são marcados como confidenciais. A marcação dos nós XML é controlada pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e não pode ser alterada pelos usuários.  
  
-   Qualquer variável marcada como confidencial. A marcação de variáveis é controlada pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Se o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] considera uma propriedade como confidencial, dependerá do desenvolvedor do componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , como um gerenciador de conexão ou tarefa, ter designado a propriedade como confidencial. Os usuários não podem adicionar propriedades à lista de propriedades, nem removê-las, porque são consideradas confidenciais.  
  
## <a name="encryption"></a>Criptografia  
 A criptografia, conforme usada pelos níveis de proteção do pacote, é executada usando a DPAPI (API de Proteção de Dados) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , que faz parte da CryptoAPI (Interface de programação de aplicativo de criptografia).  
  
 Os níveis de proteção do pacote que criptografam pacotes usando senhas também exigem que você forneça uma senha. Se o nível de proteção for alterado, de um nível que não usa uma senha para um que usa, você será solicitado a fornecer uma senha.  
  
 Além disso, para os níveis de proteção que usam uma senha, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa o algoritmo de criptografia DES triplo com um comprimento de chave de 192 bits, disponível na FCL (Biblioteca de classes do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ).  
  
## <a name="protection-levels"></a>Níveis de proteção  
 A tabela a seguir descreve os níveis de proteção que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oferece. Os valores entre parênteses são valores da enumeração do <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel> . Esses valores são exibidos na janela Propriedades usada para configurar as propriedades do pacote ao trabalhar com pacotes no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
|Nível de proteção|DESCRIÇÃO|  
|----------------------|-----------------|  
|Não salvar dados confidenciais (**DontSaveSensitive**)|Elimina os valores das propriedades confidenciais no pacote quando o pacote é salvo. Este nível de proteção não criptografa dados, em vez disso impede que as propriedades marcadas como confidenciais sejam salvas com o pacote e, consequentemente, tornam os dados confidenciais indisponíveis para os outros usuários. Se um usuário diferente abrir o pacote, as informações confidenciais serão substituídas por espaços em branco e o usuário precisará fornecer as informações confidenciais.<br /><br /> Quando usado com o utilitário **dtutil** (dtutil.exe), esse nível de proteção corresponde ao valor de 0.|  
|Criptografar tudo com senha (**EncryptAllWithPassword**)|Usa uma senha para criptografar todo o pacote. O pacote é criptografado usando uma senha fornecida pelo usuário quando o pacote é criado ou exportado. Para abrir o pacote no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer ou executá-lo com o utilitário de prompt de comando **dtexec** o usuário deve fornecer a senha do pacote. Sem a senha o usuário não pode acessar ou executar o pacote.<br /><br /> Quando usado com o utilitário **dtutil** , esse nível de proteção corresponde ao valor de 3.|  
|Criptografar tudo com chave de usuário (**EncryptAllWithUserKey**)|Usa uma chave baseada no perfil do usuário atual para criptografar todo o pacote. Apenas o usuário que criou ou exportou o pacote pode abrir o pacote no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer ou executá-lo com o utilitário de prompt de comando **dtexec** .<br /><br /> Quando usado com o utilitário **dtutil** , esse nível de proteção corresponde ao valor de 4.<br /><br /> Observação: para os níveis de proteção que usam uma chave de usuário, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa os padrões DPAPI. Para obter mais informações sobre o DPAPI, consulte a Biblioteca do MSDN em [https://msdn.microsoft.com/library](https://go.microsoft.com/fwlink/?LinkId=15408).|  
|Criptografar dados confidenciais com senha (**EncryptSensitiveWithPassword**)|Usa uma senha para criptografar apenas os valores de propriedades confidenciais no pacote. O DPAPI é usado para essa criptografia. Os dados confidenciais são salvos como parte do pacote, mas esses dados são criptografados usando uma senha que o usuário atual fornece quando o pacote é criado ou exportado. Para abrir o pacote no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , o usuário precisa fornecer a senha do pacote. Se a senha não for fornecida, o pacote será aberto sem os dados confidenciais e o usuário atual deverá fornecer valores novos para os dados confidenciais. Se o usuário tentar executar o pacote sem fornecer a senha, a execução do pacote não terá êxito. Para obter mais informações sobre senhas e execução de linha de comandos, consulte [dtexec Utility](../../integration-services/packages/dtexec-utility.md).<br /><br /> Quando usado com o utilitário **dtutil** , esse nível de proteção corresponde ao valor de 2.|  
|Criptografar dados confidenciais com chave de usuário (**EncryptSensitiveWithUserKey**)|Usa uma chave baseada no perfil do usuário atual para criptografar apenas os valores das propriedades confidenciais do pacote. Apenas o mesmo usuário que usa o mesmo perfil pode carregar o pacote. Se um usuário diferente abrir o pacote, as informações confidenciais serão substituídas por espaços em branco e o usuário atual deverá fornecer novos valores para os dados confidenciais. Se o usuário tentar executar o pacote, a execução de pacote não terá êxito. O DPAPI é usado para essa criptografia.<br /><br /> Quando usado com o utilitário **dtutil** , esse nível de proteção corresponde ao valor de 1.<br /><br /> Observação: para os níveis de proteção que usam uma chave de usuário, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa os padrões DPAPI. Para obter mais informações sobre o DPAPI, consulte a Biblioteca do MSDN em [https://msdn.microsoft.com/library](https://go.microsoft.com/fwlink/?LinkId=15408).|  
|Depender do armazenamento do servidor para criptografia (**ServerStorage**)|Protege o pacote inteiro usando funções do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Há suporte para essa opção quando um pacote é salvo no banco de dados msdb do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Somado a isso, o catálogo SSISDB usa o nível de proteção **ServerStorage** .<br /><br /> Essa opção não tem suporte quando um pacote é salvo no sistema de arquivos no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|  
  
## <a name="protection-level-setting-and-the-ssisdb-catalog"></a>Definição do nível de proteção e o catálogo SSISDB  
 O catálogo SSISDB usa o nível de proteção **ServerStorage** . Quando você implantar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o catálogo criptografará automaticamente os dados do pacote e os valores confidenciais. O catálogo também descriptografa automaticamente os dados quando você recupera-os.  
  
 Se você exportar o projeto (arquivo .ispac) do servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o sistema de arquivos, o sistema automaticamente alterará o nível de proteção para **EncryptSensitiveWithUserKey**. Se você importar o projeto usando o **Assistente de Importação de Projeto do Integration Services** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a propriedade **ProtectionLevel** na janela **Propriedades** mostrará um valor **EncryptSensitiveWithUserKey**.  
  
## <a name="protection-level-setting-based-on-package-life-cycle"></a>Configuração do nível de proteção com base no ciclo de vida do pacote  
 Você define o nível de proteção de um pacote do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] quando o desenvolve pela primeira vez no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Posteriormente, quando o pacote for implantado, importado ou exportado do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou copiado do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o Armazenamento de Pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou o sistema de arquivos, você poderá atualizar o nível de proteção do pacote. Por exemplo, se você criar e salvar pacotes no computador com uma das opções de nível de proteção de chave de usuário, provavelmente precisará alterar o nível de proteção ao fornecer o pacote a outros usuários; caso contrário eles não poderão abrir o pacote.  
  
 Em geral, você altera o nível de proteção conforme listado nas seguintes etapas:  
  
1.  Durante o desenvolvimento, deixe o nível de proteção de pacotes definido como o valor padrão, **EncryptSensitiveWithUserKey**. Essa configuração ajuda a garantir que somente o desenvolvedor veja os valores confidenciais no pacote. Ou, você pode considerar o uso de **EncryptAllWithUserKey**ou de **DontSaveSensitive**.  
  
2.  Na hora de implantar os pacotes, você precisa alterar o nível de proteção para um que não dependa da chave de usuário do desenvolvedor. Portanto, normalmente, você precisa selecionar **EncryptSensitiveWithPassword**ou **EncryptAllWithPassword**. Criptografe os pacotes atribuindo uma senha forte temporária que também seja conhecida pela equipe de operações no ambiente de produção.  
  
3.  Após a implantação dos pacotes no ambiente de produção, a equipe de operações pode criptografar novamente os pacotes implantados atribuindo uma senha forte conhecida somente por eles. Ou, eles podem criptografar os pacotes implantados selecionando **EncryptSensitiveWithUserKey** ou **EncryptAllWithUserKey**e usando as credenciais locais da conta que executará os pacotes.  

## <a name="set-or-change-the-protection-level-of-packages"></a><a name="set_protection"></a> Definir ou alterar o nível de proteção de pacotes
  Para controlar o acesso ao conteúdo de pacotes e aos valores confidenciais que eles contêm, como senhas, defina o valor da propriedade **ProtectionLevel** . Os pacotes contidos em um projeto precisam ter o mesmo nível de proteção que o projeto, para criar o projeto. Se você alterou a configuração de propriedade **ProtectionLevel** no projeto, precisa atualizar manualmente a configuração da propriedade para os pacotes.  
  
 Para obter uma visão geral dos recursos de segurança no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Visão geral de segurança &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md).  
  
 Os procedimentos deste tópico descrevem como usar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou o utilitário de prompt de comando dtutil para alterar a propriedade **ProtectionLevel** .  
  
> [!NOTE]  
>  Além dos procedimentos deste tópico, normalmente você pode definir ou alterar a propriedade **ProtectionLevel** de um pacote ao importar ou exportar o pacote. Você também pode alterar a propriedade de **ProtectionLevel** de um pacote ao usar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para salvar um pacote.  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>Para definir ou alterar o nível de proteção de um pacote nas Ferramentas de Dados do SQL Server  
  
1.  Examine os valores disponíveis para a propriedade **ProtectionLevel** na seção [Níveis de proteção](#protection-levels) e determine o valor apropriado do pacote.  
  
2.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote.  
  
3.  Abra o pacote no designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
4.  Se a janela Propriedades não mostrar as propriedades do pacote, clique na superfície de design.  
  
5.  Na janela Propriedades, no grupo **Segurança** , selecione o valor apropriado para a propriedade **ProtectionLevel** .  
  
     Se você selecionar um nível de proteção que exija uma senha, insira a senha como o valor da propriedade **PackagePassword** .  
  
6.  No menu **Arquivo** , selecione **Salvar Itens Selecionados** para salvar o pacote modificado.  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>Para definir ou alterar o nível de proteção de pacotes no prompt de comando  
  
1.  Examine os valores disponíveis para a propriedade **ProtectionLevel** na seção [Níveis de proteção](#protection-levels) e determine o valor apropriado do pacote.  
  
2.  Examine os mapeamentos para a opção **Encrypt** no tópico [dtutil Utility](../../integration-services/dtutil-utility.md)e determine o inteiro apropriado a ser usado como o valor da propriedade **ProtectionLevel** selecionada.  
  
3.  Abra uma janela de Prompt de Comando.  
  
4.  No prompt de comando, navegue para a pasta que contém o pacote ou pacotes para os quais você deseja definir a propriedade **ProtectionLevel** .  
  
     Os exemplos de sintaxe mostrados na etapa a seguir assumem que essa é a pasta atual.  
  
5.  Defina ou altere o nível de proteção do pacote ou pacotes usando um comando semelhante ao dos seguintes exemplos:  
  
    -   O comando a seguir define a propriedade **ProtectionLevel** de um pacote individual no sistema de arquivos como nível 2, "Criptografar dados confidenciais com senha", com a senha "senha forte":  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   O comando a seguir define a propriedade **ProtectionLevel** de todos os pacotes em uma pasta específica no sistema de arquivos como nível 2, "Criptografar dados confidenciais com senha", com a senha "senha forte":  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         Se você usar um comando semelhante em um arquivo em lotes, digite o espaço reservado do arquivo, "%f", como "%%f" no arquivo em lotes.  

## <a name="package-project-protection-level-dialog-box"></a><a name="protection_dialog"></a> Caixa de diálogo Nível de Proteção do Projeto de Pacote
  Use a caixa de diálogo **Nível de Proteção do Pacote** para atualizar o nível de proteção de um pacote. O nível de proteção determina o método de proteção, a senha ou a chave de usuário, bem como o escopo de proteção do pacote. A proteção pode incluir todos os dados ou apenas os dados confidenciais.  
  
 Para entender os requisitos e as opções de segurança de pacote, pode ser útil consultar [Visão geral de segurança &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md).  
  
### <a name="options"></a>Opções  
 **Nível de Proteção do Pacote**  
 Selecione um nível de proteção na lista.  
  
 **Senha**  
 Se você estiver usando o nível de proteção **Criptografar dados confidenciais com senhas** ou **Criptografar todos os dados com senhas** , digite uma senha.  
  
 **Digite a senha novamente**  
 Digite a senha novamente.  

## <a name="package-password-dialog-box"></a><a name="password_dialog"></a> Caixa de diálogo Senha do Pacote
  Use a caixa de diálogo **Senha do Pacote** para digitar a senha de um pacote criptografado com uma senha. É necessário digitar uma senha se o pacote usar o nível de proteção **Criptografar dados confidenciais com senha**ou **Criptografar tudo com senha** .  
  
### <a name="options"></a>Opções  
 **Senha**  
 Digite a senha.  
  
## <a name="see-also"></a>Consulte Também  
 [Pacotes do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)   
 [Visão geral de segurança &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
 [Utilitário dtutil](../../integration-services/dtutil-utility.md)  
  
