---
title: Importar e exportar pacotes (serviço SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], importing
- packages [Integration Services], exporting
- importing packages
- exporting packages
ms.assetid: ef18ec11-b536-47d9-abd1-794099f43486
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ce04befcb4c8558216cecded6cb1892c3106295f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965666"
---
# <a name="import-and-export-packages-ssis-service"></a>Importar e exportar pacotes (serviço SSIS)
    
> [!IMPORTANT]  
>  Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
 Os pacotes podem ser salvos na tabela sysssispackages no banco de dados msdb do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou no sistema de arquivos.  
  
 O repositório de pacotes, que é o armazenamento lógico que o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] monitora e gerencia, pode incluir o banco de dados msdb e as pastas do sistema de arquivos especificadas no arquivo de configuração para o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Você pode importar e exportar pacotes entre os seguintes tipos de armazenamento:  
  
-   Pastas do sistema de arquivos em qualquer lugar do sistema de arquivos.  
  
-   Pastas no repositório de pacotes SSIS. As duas pastas padrão são nomeadas Sistema de Arquivos e MSDB.  
  
-   O banco de dados msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] permite importar e exportar pacotes e, ao fazer isso, alterar o formato de armazenamento e o local de pacotes. Usando os recursos de importação e exportação, você pode adicionar pacotes ao sistema de arquivos, ao repositório de pacotes ou ao banco de dados msdb e copiar pacotes de um formato de armazenamento para outro. Por exemplo, os pacotes salvos no msdb podem ser copiados para o sistema de arquivos e vice-versa.  
  
 Você também pode copiar um pacote em um formato diferente por meio do utilitário do prompt de comando **dtutil** (dtutil.exe). Para obter mais informações, consulte [dtutil Utility](dtutil-utility.md).  
  
## <a name="to-import-or-export-a-package"></a>Para importar ou exportar um pacote  
  
> [!IMPORTANT]  
>  Este tópico discute o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que faz parte do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] dá suporte ao serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para compatibilidade de versões anteriores com o [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Para obter mais informações sobre o gerenciamento de pacotes no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], consulte [Servidor do Integration Services &#40;SSIS&#41;](catalog/integration-services-ssis-server-and-catalog.md).  
  
 Você pode importar ou exportar um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de ou para os seguintes locais:  
  
-   Você pode importar um pacote armazenado em uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , no sistema de arquivos ou no [!INCLUDE[ssIS](../includes/ssis-md.md)] repositório de pacotes. O pacote importado é salvo no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou em uma pasta do armazenamento de pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   É possível exportar um pacote armazenado em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], no sistema de arquivos ou no Repositório de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] para outro formato e outro local de armazenamento.  
  
 No entanto, existem algumas restrições sobre a importação e a exportação de pacotes entre diferentes versões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Em uma instância do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], você pode importar pacotes de uma instância do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], mas não é possível exportar pacotes para uma instância do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)].  
  
-   Em uma instância do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], você não pode importar pacotes de, ou exportar pacotes para, uma instância do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
 Os procedimentos a seguir descrevem como usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para importar ou exportar um pacote.  
  
#### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>Para importar um pacote usando o SQL Server Management Studio  
  
1.  Clique em **Iniciar**, aponte para **Microsoft** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e clique em **SQL Server Management Studio**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , defina as seguintes opções:  
  
    -   Na caixa **Tipo de servidor** , selecione **Integration Services**.  
  
    -   Na caixa **nome do servidor** , forneça um nome de servidor ou clique **\<Browse for more...>** e localize o servidor a ser usado.  
  
3.  Se o Pesquisador de Objetos não estiver aberto, clique em **Pesquisador de Objetos** no menu **Exibir**.  
  
4.  No Pesquisador de objetos, expanda a pasta **pacotes armazenados** .  
  
5.  Expanda as subpastas para localizar a pasta para a qual você deseja importar um pacote.  
  
6.  Clique com o botão direito do mouse na pasta e clique em **Importar Pacote**. Em seguida, proceda de uma das seguintes maneiras:  
  
    -   Para importar de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], selecione a opção **SQL Server** e depois especifique o servidor e selecione o modo de autenticação. Se você selecionar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , forneça um nome de usuário e uma senha.  
  
         Clique no botão Procurar **(...)**, selecione o pacote para importar e clique em **OK.**  
  
    -   Para importar do sistema de arquivos, selecione a opção **Sistema de arquivos** .  
  
         Clique no botão Procurar **(...)**, selecione o pacote para importar e então clique em **Abrir.**  
  
    -   Para importar usando o Repositório de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] , selecione a opção **Repositório de Pacotes SSIS** e especifique o servidor.  
  
         Clique no botão Procurar **(...)**, selecione o pacote para importar e clique em **OK.**  
  
7.  Opcionalmente, atualize o nome de pacote.  
  
8.  Para atualizar o nível de proteção do pacote, clique no botão Procurar **(...)** e, na caixa de diálogo **Nível de Proteção do Pacote**, escolha um nível de proteção diferente. Se a opção **Criptografar dados confidenciais com senhas** ou **Criptografar todos os dados com senhas** for selecionada, digite e confirme uma senha.  
  
9. Clique em **OK** para concluir a importação.  
  
#### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>Para exportar um pacote usando o SQL Server Management Studio  
  
1.  Clique em **Iniciar**, aponte para **Microsoft** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e clique em **SQL Server Management Studio**.  
  
2.  Na caixa de diálogo **conectar ao servidor** , defina as seguintes opções:  
  
    -   Na caixa **Tipo de servidor** , selecione **Integration Services**.  
  
    -   Na caixa **nome do servidor** , forneça um nome de servidor ou clique **\<Browse for more...>** e localize o servidor a ser usado.  
  
3.  Se o Pesquisador de Objetos não estiver aberto, clique em **Pesquisador de Objetos** no menu **Exibir**.  
  
4.  No Pesquisador de objetos, expanda a pasta **pacotes armazenados** .  
  
5.  Expanda as subpastas para localizar o pacote que deseja exportar.  
  
6.  Clique com o botão direito do mouse no pacote, clique em **Exportar**e depois execute uma das seguintes tarefas:  
  
    -   Para exportar para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], selecione a opção **SQL Server** e depois especifique o servidor e selecione o modo de autenticação. Se você selecionar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , forneça um nome de usuário e uma senha.  
  
         Clique no botão Procurar **(...)** e expanda a pasta do **Pacotes SSIS** para localizar a pasta na qual deseja salvar o pacote. Opcionalmente, atualize o nome padrão do pacote e então clique em **OK**.  
  
    -   Para exportar para o sistema de arquivos, selecione a opção **Sistema de Arquivos** .  
  
         Clique no botão Procurar **(...)** para localizar a pasta para a qual deseja exportar o pacote, digite o nome do arquivo do pacote e clique em **Salvar**.  
  
    -   Para exportar para o repositório de pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] , selecione a opção **Repositório de Pacotes SISS** e especifique o servidor.  
  
         Clique no botão Procurar **(...)**, expanda a pasta dos **Pacotes SSIS** e selecione a pasta na qual deseja salvar o pacote. Opcionalmente, digite um novo nome para o pacote na caixa de texto **Nome do Pacote** . [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Para atualizar o nível de proteção do pacote, clique no botão Procurar **(...)** e, na caixa de diálogo **Nível de Proteção do Pacote**, escolha um nível de proteção diferente. Se a opção **Criptografar dados confidenciais com senhas** ou **Criptografar todos os dados com senhas** for selecionada, digite e confirme uma senha.  
  
8.  Clique em **OK** para completar a exportação.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](service/package-management-ssis-service.md)  
  
  
