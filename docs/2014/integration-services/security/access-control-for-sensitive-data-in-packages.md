---
title: Controle de acesso de dados confidenciais em pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services], security
- protection levels for packages [Integration Services]
- configuration files [Integration Services]
- encryption [Integration Services]
- cryptography [Integration Services]
- security [Integration Services], protection levels
ms.assetid: d4b073c4-4238-41fc-a258-4e114216e185
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d59a42fa7b77e6800218f1eeca4986320c1dcef
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379934"
---
# <a name="access-control-for-sensitive-data-in-packages"></a>Controle de acesso de dados confidenciais em pacotes
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
  
|Nível de proteção|Descrição|  
|----------------------|-----------------|  
|Não salvar dados confidenciais (`DontSaveSensitive`)|Elimina os valores das propriedades confidenciais no pacote quando o pacote é salvo. Este nível de proteção não criptografa dados, em vez disso impede que as propriedades marcadas como confidenciais sejam salvas com o pacote e, consequentemente, tornam os dados confidenciais indisponíveis para os outros usuários. Se um usuário diferente abrir o pacote, as informações confidenciais serão substituídas por espaços em branco e o usuário precisará fornecer as informações confidenciais.<br /><br /> Quando usado com o utilitário **dtutil** (dtutil.exe), esse nível de proteção corresponde ao valor de 0.|  
|Criptografar tudo com senha (`EncryptAllWithPassword`)|Usa uma senha para criptografar todo o pacote. O pacote é criptografado usando uma senha fornecida pelo usuário quando o pacote é criado ou exportado. Para abrir o pacote no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer ou executá-lo com o utilitário de prompt de comando **dtexec** o usuário deve fornecer a senha do pacote. Sem a senha o usuário não pode acessar ou executar o pacote.<br /><br /> Quando usado com o utilitário **dtutil** , esse nível de proteção corresponde ao valor de 3.|  
|Criptografar tudo com chave de usuário (`EncryptAllWithUserKey`)|Usa uma chave baseada no perfil do usuário atual para criptografar todo o pacote. Apenas o usuário que criou ou exportou o pacote pode abrir o pacote no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer ou executá-lo com o utilitário de prompt de comando **dtexec** .<br /><br /> Quando usado com o utilitário **dtutil** , esse nível de proteção corresponde ao valor de 4.<br /><br /> Observação: Para os níveis de proteção que usam uma chave de usuário, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa os padrões DPAPI. Para obter mais informações sobre o DPAPI, consulte a Biblioteca do MSDN em [https://msdn.microsoft.com/library](https://go.microsoft.com/fwlink/?LinkId=15408).|  
|Criptografar dados confidenciais com senha (`EncryptSensitiveWithPassword`)|Usa uma senha para criptografar apenas os valores de propriedades confidenciais no pacote. O DPAPI é usado para essa criptografia. Os dados confidenciais são salvos como parte do pacote, mas esses dados são criptografados usando uma senha que o usuário atual fornece quando o pacote é criado ou exportado. Para abrir o pacote no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , o usuário precisa fornecer a senha do pacote. Se a senha não for fornecida, o pacote será aberto sem os dados confidenciais e o usuário atual deverá fornecer valores novos para os dados confidenciais. Se o usuário tentar executar o pacote sem fornecer a senha, a execução do pacote não terá êxito. Para obter mais informações sobre senhas e execução de linha de comandos, consulte [dtexec Utility](../packages/dtexec-utility.md).<br /><br /> Quando usado com o utilitário **dtutil** , esse nível de proteção corresponde ao valor de 2.|  
|Criptografar dados confidenciais com chave de usuário (`EncryptSensitiveWithUserKey`)|Usa uma chave baseada no perfil do usuário atual para criptografar apenas os valores das propriedades confidenciais do pacote. Apenas o mesmo usuário que usa o mesmo perfil pode carregar o pacote. Se um usuário diferente abrir o pacote, as informações confidenciais serão substituídas por espaços em branco e o usuário atual deverá fornecer novos valores para os dados confidenciais. Se o usuário tentar executar o pacote, a execução de pacote não terá êxito. O DPAPI é usado para essa criptografia.<br /><br /> Quando usado com o utilitário **dtutil** , esse nível de proteção corresponde ao valor de 1.<br /><br /> Observação: Para os níveis de proteção que usam uma chave de usuário, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa os padrões DPAPI. Para obter mais informações sobre o DPAPI, consulte a Biblioteca do MSDN em [https://msdn.microsoft.com/library](https://go.microsoft.com/fwlink/?LinkId=15408).|  
|Depender do armazenamento do servidor para criptografia (`ServerStorage`)|Protege o pacote inteiro usando funções do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Há suporte para essa opção quando um pacote é salvo no banco de dados msdb do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Somado a isso, o catálogo SSISDB usa o nível de proteção `ServerStorage`.<br /><br /> Essa opção não tem suporte quando um pacote é salvo no sistema de arquivos no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|  
  
## <a name="protection-level-setting-and-the-ssisdb-catalog"></a>Definição do nível de proteção e o catálogo SSISDB  
 O catálogo SSISDB usa o nível de proteção `ServerStorage`. Quando você implantar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o catálogo criptografará automaticamente os dados do pacote e os valores confidenciais. O catálogo também descriptografa automaticamente os dados quando você recupera-os.  
  
 Se você exportar o projeto (arquivo .ispac) do servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o sistema de arquivos, o sistema automaticamente alterará o nível de proteção para `EncryptSensitiveWithUserKey`. Se você importar o projeto usando o **Assistente de projeto importar do Integration Services** na [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o **ProtectionLevel** propriedade no **propriedades** janela mostra um valor de `EncryptSensitiveWithUserKey`.  
  
## <a name="protection-level-setting-based-on-package-life-cycle"></a>Configuração do nível de proteção com base no ciclo de vida do pacote  
 Você define o nível de proteção de um pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] quando o desenvolve primeiro no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Posteriormente, quando o pacote for implantado, importado ou exportado do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou copiado do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o Armazenamento de Pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou o sistema de arquivos, você poderá atualizar o nível de proteção do pacote. Por exemplo, se você criar e salvar pacotes no computador com uma das opções de nível de proteção de chave de usuário, provavelmente precisará alterar o nível de proteção ao fornecer o pacote a outros usuários; caso contrário eles não poderão abrir o pacote.  
  
 Em geral, você altera o nível de proteção conforme listado nas seguintes etapas:  
  
1.  Durante o desenvolvimento, deixe o nível de proteção de pacotes definido como o valor padrão, `EncryptSensitiveWithUserKey`. Essa configuração ajuda a garantir que somente o desenvolvedor veja os valores confidenciais no pacote. Ou, você pode considerar o uso de `EncryptAllWithUserKey` ou de `DontSaveSensitive`.  
  
2.  Na hora de implantar os pacotes, você precisa alterar o nível de proteção para um que não dependa da chave de usuário do desenvolvedor. Portanto, normalmente, você precisa selecionar `EncryptSensitiveWithPassword` ou `EncryptAllWithPassword`. Criptografe os pacotes atribuindo uma senha forte temporária que também seja conhecida pela equipe de operações no ambiente de produção.  
  
3.  Após a implantação dos pacotes no ambiente de produção, a equipe de operações pode criptografar novamente os pacotes implantados atribuindo uma senha forte conhecida somente por eles. Ou, eles podem criptografar os pacotes implantados selecionando `EncryptSensitiveWithUserKey` ou `EncryptAllWithUserKey` e usando as credenciais locais da conta que executará os pacotes.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Definir ou alterar o nível de proteção de pacotes](../set-or-change-the-protection-level-of-packages.md)  
  
## <a name="see-also"></a>Consulte também  
 [Importar e exportar pacotes &#40;Serviço SSIS&#41;](../import-and-export-packages-ssis-service.md)   
 [Pacotes do Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md)   
 [Visão geral de segurança &#40;Integration Services&#41;](security-overview-integration-services.md)  
  
  
