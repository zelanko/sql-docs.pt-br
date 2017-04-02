---
title: "Definir ou alterar o n&#237;vel de prote&#231;&#227;o de pacotes | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "senhas [Integration Services]"
  - "pacotes [Integration Services], segurança"
  - "segurança [Integration Services], níveis de proteção"
  - "nível de proteção para pacotes [Integration Services]"
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Definir ou alterar o n&#237;vel de prote&#231;&#227;o de pacotes
  Para controlar o acesso ao conteúdo de pacotes e aos valores confidenciais que eles contêm, como senhas, defina o valor da propriedade **ProtectionLevel**. Os pacotes contidos em um projeto precisam ter o mesmo nível de proteção que o projeto, para criar o projeto. Se você alterou a configuração de propriedade **ProtectionLevel** no projeto, precisa atualizar manualmente a configuração da propriedade para os pacotes.  
  
 Para obter informações sobre como determinar as configurações de **ProtectionLevel** apropriadas para pacotes em diferentes fases do ciclo de vida do pacote, consulte [Controle de acesso para dados confidenciais em pacotes](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md). Para obter uma visão geral dos recursos de segurança no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Visão geral de segurança &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md).  
  
 Os procedimentos deste tópico descrevem como usar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou o utilitário de prompt de comando dtutil para alterar a propriedade **ProtectionLevel**.  
  
> [!NOTE]  
>  Além dos procedimentos deste tópico, normalmente você pode definir ou alterar a propriedade **ProtectionLevel** de um pacote ao importar ou exportar o pacote. Você também pode alterar a propriedade de **ProtectionLevel** de um pacote ao usar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para salvar um pacote.  
  
### Para definir ou alterar o nível de proteção de um pacote nas Ferramentas de Dados do SQL Server  
  
1.  Examine os valores disponíveis da propriedade **ProtectionLevel** no tópico [Definindo o nível de proteção de pacotes](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md) e determine o valor apropriado do pacote.  
  
2.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote.  
  
3.  Abra o pacote no designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
4.  Se a janela Propriedades não mostrar as propriedades do pacote, clique na superfície de design.  
  
5.  Na janela Propriedades, no grupo **Segurança**, selecione o valor apropriado para a propriedade **ProtectionLevel**.  
  
     Se você selecionar um nível de proteção que exija uma senha, insira a senha como o valor da propriedade **PackagePassword**.  
  
6.  No menu **Arquivo**, selecione **Salvar Itens Selecionados** para salvar o pacote modificado.  
  
### Para definir ou alterar o nível de proteção de pacotes no prompt de comando  
  
1.  Examine os valores disponíveis da propriedade **ProtectionLevel** no tópico [Definindo o nível de proteção de pacotes](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md) e determine o valor apropriado do pacote.  
  
2.  Examine os mapeamentos para a opção **Encrypt** no tópico [dtutil Utility](../../integration-services/dtutil-utility.md) e determine o inteiro apropriado a ser usado como o valor da propriedade **ProtectionLevel** selecionada.  
  
3.  Abra uma janela do prompt de comando.  
  
4.  No prompt de comando, navegue para a pasta que contém o pacote ou pacotes para os quais você deseja definir a propriedade **ProtectionLevel**.  
  
     Os exemplos de sintaxe mostrados na etapa a seguir assumem que essa é a pasta atual.  
  
5.  Defina ou altere o nível de proteção do pacote ou pacotes usando um comando semelhante ao dos seguintes exemplos:  
  
    -   O comando a seguir define a propriedade **ProtectionLevel** de um pacote individual no sistema de arquivos como nível 2, "Criptografar dados confidenciais com senha", com a senha "senha forte":  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   O comando a seguir define a propriedade **ProtectionLevel** de todos os pacotes em uma pasta específica no sistema de arquivos como nível 2, "Criptografar dados confidenciais com senha", com a senha "senha forte":  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         Se você usar um comando semelhante em um arquivo em lotes, digite o espaço reservado do arquivo, "%f", como "%%f" no arquivo em lotes.  
  
## Consulte também  
 [Utilitário dtutil](../../integration-services/dtutil-utility.md)  
  
  