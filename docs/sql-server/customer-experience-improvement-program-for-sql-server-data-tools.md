---
title: Programa de Aperfeiçoamento da Experiência do Usuário para SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 10/21/2016
ms.prod: sql
ms.prod_service: sql
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.technology: ssdt
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: baf3a205-a6bb-4564-8b64-3a0475bb9273
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 84313f1bedd406c39a862c57bdc94436eb0c7cbe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="customer-experience-improvement-program-for-sql-server-data-tools"></a>Programa de Aperfeiçoamento da Experiência do Usuário para SQL Server Data Tools
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Saiba como o Programa de Aperfeiçoamento da Experiência do Usuário ajuda a Microsoft a identificar maneiras de aperfeiçoar o nosso software.  Você pode configurar ferramentas para aceitá-las ou recusá-las a qualquer momento.  
  
> [!NOTE]  
>  Para ver uma explicação sobre as práticas de coleta e de uso de dados do usuário das versões do Microsoft SQL Server 2016 e de outros produtos e serviços, consulte esta [política de privacidade da Microsoft](https://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx).  
  
## <a name="opting-in-and-out-of-ceip-for-sql-server-data-tools"></a>Aceitar e recusar o Programa de Aperfeiçoamento da Experiência do Usuário para SQL Server Data Tools  
 O Programa de Aperfeiçoamento da Experiência do Usuário foi projetado para ajudar a Microsoft a aperfeiçoar seus produtos ao longo do tempo. Esse programa coleta informações sobre o hardware do computador e sobre como as pessoas usam nossos produtos, sem interromper as tarefas dos usuários no computador. As informações coletadas ajudam a Microsoft a identificar os recursos que devem ser melhorados. Neste documento, abordaremos como aceitar ou recusar o Programa de Aperfeiçoamento da Experiência do Usuário para SSDT (SQL Server Data Tools) para o Visual Studio 2017, Visual Studio 2015 e Visual Studio 2013.  

### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2017"></a>Opção e controle do Programa de Aperfeiçoamento da Experiência do Usuário e o SQL Server Data Tools para Visual Studio 2017  
 O SSDT para Visual Studio 2017 é a ferramenta de modelagem de dados que acompanha o SQL Server 2017. Ele usa as opções do Programa de Aperfeiçoamento da Experiência do Usuário internas do Visual Studio 2017. Saiba mais sobre como enviar comentários por meio do Programa de Aperfeiçoamento da Experiência do Usuário no Visual Studio 2017 neste [documento da ajuda do Visual Studio](https://www.visualstudio.com/en-us/docs/work/connect/give-feedback).  
  
 Para as versões prévias do SQL Server 2017, o Programa de Aperfeiçoamento da Experiência do Usuário é ativado por padrão. Para desativá-lo e ativá-lo novamente, siga as instruções abaixo.  
  
 **No Visual Studio (se aplica a instalações de idiomas completas do Visual Studio 2017)**  
  
 Quando você executa a Instalação do SSDT em um computador que já tenha o Visual Studio, apenas os modelos de projeto do SQL Server e do Business Intelligence são adicionados. Para este cenário, as opções de comentários do cliente fornecidas pelo Visual Studio podem ser usadas para aceitar ou recusar o Programa de Aperfeiçoamento da Experiência do Usuário.  
  
1.  Inicie o Visual Studio.  
  
2.  No menu Ajuda, selecione **Enviar Comentários** > **Configurações**.  
  
3.  Para desativar o CEIP, clique em **Não, prefiro não participar**e, em seguida, clique em **OK**.  
  
     Para ativar o CEIP, clique em **Sim, quero participar**e, em seguida, clique em **OK**.  
  

  
 **Usar uma política baseada no Registro ou em uma Política de Grupo**  
  
 Quando você executa a Instalação do SSDT em um computador que não tenha o Visual Studio 2017, apenas o Shell do Visual Studio é instalado. O shell não fornece opções de comentários do cliente. Nesse caso, a única opção de configuração do Programa de Aperfeiçoamento da Experiência do Usuário é uma atualização do registro  
  
 Os clientes corporativos podem criar uma Política de Grupo para aceitar ou recusar ao definirem uma política baseada no Registro para o SQL Server 2017.  
  
 Chave do Registro e configurações relevantes:  
  
 Key = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\15.0\SQM  
  
 RegEntry name = OptIn  
  
 Tipo de entrada DWORD:  
  
-   0 significa não usar  
  
-   1 significa usar  
  
> [!CAUTION]  
>  A edição incorreta do Registro poderá danificar seriamente o sistema. Antes de alterar o Registro, faça um backup dos dados importantes do computador. Você poderá também usar a opção de inicialização Última Configuração Válida se encontrar problemas depois de aplicar as alterações manualmente.  
  
 Para saber mais sobre os dados coletados, processados ou transmitidos pelo Programa de Aperfeiçoamento da Experiência do Usuário, confira a [Política de Privacidade do Programa de Aperfeiçoamento da Experiência do Usuário da Microsoft](http://go.microsoft.com/fwlink/?LinkId=52143).  
 
### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2015"></a>Opção e controle do Programa de Aperfeiçoamento da Experiência do Usuário e o SQL Server Data Tools para Visual Studio 2015  
 O SSDT para Visual Studio 2015 é a ferramenta de modelagem de dados que acompanha o SQL Server 2016. Ele usa as opções do Programa de Aperfeiçoamento da Experiência do Usuário internas do Visual Studio 2015. Saiba mais sobre como enviar comentários por meio do Programa de Aperfeiçoamento da Experiência do Usuário no Visual Studio 2015 neste [documento da Ajuda do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=517102).  
  
 Para as versões anteriores ao SQL Server 2016, o Programa de Aperfeiçoamento da Experiência do Usuário é ativado por padrão. Para desativá-lo e ativá-lo novamente, siga as instruções abaixo.  
  
 **No Visual Studio (se aplica a instalações de idiomas completas do Visual Studio 2015)**  
  
 Quando você executa a Instalação do SSDT em um computador que já tenha o Visual Studio, apenas os modelos de projeto do SQL Server e do Business Intelligence são adicionados. Para este cenário, as opções de comentários do cliente fornecidas pelo Visual Studio podem ser usadas para aceitar ou recusar o Programa de Aperfeiçoamento da Experiência do Usuário.  
  
1.  Inicie o Visual Studio.  
  
2.  No menu Ajuda, selecione **Enviar Comentários** > **Configurações**.  
  
3.  Para desativar o CEIP, clique em **Não, prefiro não participar**e, em seguida, clique em **OK**.  
  
     Para ativar o CEIP, clique em **Sim, quero participar**e, em seguida, clique em **OK**.  
  

  
 **Usar uma política baseada no Registro ou em uma Política de Grupo**  
  
 Quando você executa a Instalação do SSDT em um computador que não tenha o Visual Studio 2015, apenas o Shell do Visual Studio é instalado. O shell não fornece opções de comentários do cliente. Nesse caso, a única opção de configuração do Programa de Aperfeiçoamento da Experiência do Usuário é uma atualização do registro  
  
 Os clientes corporativos podem criar uma Política de Grupo para aceitar ou recusar o Programa de Aperfeiçoamento da Experiência do Usuário através da configuração de uma política baseada no Registro para o SQL Server 2016.  
  
 Chave do Registro e configurações relevantes:  
  
 Key = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\14.0\SQM  
  
 RegEntry name = OptIn  
  
 Tipo de entrada DWORD:  
  
-   0 significa não usar  
  
-   1 significa usar  
  
> [!CAUTION]  
>  A edição incorreta do Registro poderá danificar seriamente o sistema. Antes de alterar o Registro, faça um backup dos dados importantes do computador. Você poderá também usar a opção de inicialização Última Configuração Válida se encontrar problemas depois de aplicar as alterações manualmente.  
  
 Para saber mais sobre os dados coletados, processados ou transmitidos pelo Programa de Aperfeiçoamento da Experiência do Usuário, confira a [Política de Privacidade do Programa de Aperfeiçoamento da Experiência do Usuário da Microsoft](http://go.microsoft.com/fwlink/?LinkId=52143).  
  
### <a name="choice-and-control-for-ceip-and-sql-server-data-tools---bi-ssdt-bi"></a>Escolha e controle para o Programa de Aperfeiçoamento da Experiência do Usuário e o SQL Server Data Tools – BI (SSDT-BI)  
 Se estiver usando o SSDT-BI, você terá uma oportunidade de participar do Programa de Aperfeiçoamento da Experiência do Usuário durante a instalação. Posteriormente, você pode fazer alterações na configuração do Programa de Aperfeiçoamento da Experiência do Usuário para o SSDT-BI usando ferramentas de cliente ou editando as configurações do registro.  
  
 **No SSDT e no SSDT-BI para Visual Studio 2013**  
  
1.  Inicie a ferramenta e abra um projeto novo ou um existente do Analysis Services ou do Integration Services.  
  
2.  No menu Ajuda, escolha **Opções de Comentários do Cliente do Microsoft SQL Server**.  
  
3.  Para desabilitar o Programa de Aperfeiçoamento da Experiência do Usuário, clique em **Não, eu não desejo participar**.  
  
     Para habilitar o Programa de Aperfeiçoamento da Experiência do Usuário, clique em **Sim, desejo participar**.  
  
4.  Clique em **OK**.  
  
 **Usar uma política baseada no Registro ou em uma Política de Grupo**  
  
 Os clientes corporativos podem criar uma Política de Grupo para aceitar ou recusar ao definirem uma política baseada no Registro para o SQL Server 2014.  
  
 Chave do Registro e configurações relevantes:  
  
 Chave = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\120  
  
 Nome da RegEntry = CustomerFeedback  
  
 Tipo de entrada DWORD:  
  
-   0 significa não usar  
  
-   1 significa usar  
  
  
