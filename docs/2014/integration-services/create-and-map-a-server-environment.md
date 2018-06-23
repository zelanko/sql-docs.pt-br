---
title: Criar e mapear um ambiente de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.ssms.isenvprop.variables.f1
- sql12.ssis.ssms.iscreateenv.f1
- sql12.ssis.ssms.isenvprop.permissions.f1
- sql12.ssis.ssms.isenvprop.general.f1
ms.assetid: b1cbb697-713f-48e4-b234-b23724d87451
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7b386dd13218d78bc8b70dacba6a0103bf9a8581
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013155"
---
# <a name="create-and-map-a-server-environment"></a>Criar e mapear um ambiente de servidor
  Você cria um ambiente de servidor para especificar valores de tempo de execução para pacotes contidos em um projeto que você implantou no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Você pode mapear as variáveis de ambiente para parâmetros, para um pacote específico, para pacotes de ponto de entrada ou para todos os pacotes em um projeto específico. Um pacote de ponto de entrada é geralmente um pacote pai que executa um pacote filho.  
  
> [!IMPORTANT]  
>  Para uma execução específica, um pacote pode ser executado somente com os valores contidos em um único ambiente de servidor.  
  
 Você pode consultar as exibições para uma lista de ambientes de servidor, referências de ambiente e variáveis de ambiente. Você também pode chamar procedimentos armazenados para adicionar, excluir, alterar e modificar ambientes, referências de ambiente e variáveis de ambiente. Para obter mais informações, consulte a seção **Ambientes de servidor, variáveis de servidor e referências de ambiente de servidor** em [SSIS Catalog](catalog/ssis-catalog.md).  
  
### <a name="to-create-and-use-a-server-environment"></a>Para criar e usar um ambiente de servidor  
  
1.  No [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], expanda o nó [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Catálogos> **SSISDB** no Pesquisador de Objetos e localize a pasta **Ambientes** do projeto por meio do qual você quer criar um ambiente.  
  
2.  Clique com o botão direito do mouse na pasta **Ambientes** e clique em **Criar Ambiente**.  
  
3.  Digite um nome para o ambiente e uma descrição (opcional) e clique em **OK**.  
  
4.  Clique com o botão direito do mouse no novo ambiente e clique em **Propriedades**.  
  
5.  Na página **Variáveis** , faça o seguinte para adicionar uma variável.  
  
    1.  Selecione o **Tipo** da variável. O nome da variável **não** precisa corresponder ao nome do parâmetro do projeto que você mapeará para a variável.  
  
    2.  Digite uma **Descrição** opcional para a variável.  
  
    3.  Digite o **Valor** para a variável de ambiente.  
  
         Para obter informações sobre as regras para nomes de variável de ambiente, consulte a seção **Variável do ambiente** em [SSIS Catalog](catalog/ssis-catalog.md).  
  
    4.  Indica se a variável contém o valor confidencial, marcando ou desmarcando a caixa de seleção **Confidencial** .  
  
         Se você selecionar **Confidencial**, o valor da variável não será exibido no campo **Valor** .  
  
         Os valores confidenciais são criptografados no catálogo do SSISDB. Para obter mais informações sobre a criptografia SSL, consulte [SSIS Catalog](catalog/ssis-catalog.md).  
  
6.  Na página **Permissões** , conceda ou negue permissões para usuários e funções selecionados fazendo o seguinte.  
  
    1.  Clique em **Procurar**e selecione um ou mais usuários e funções na caixa de diálogo **Procurar Todas as Entidades de Segurança** .  
  
    2.  Na área **Logons ou funções** , selecione o usuário ou função ao qual você quer conceder ou negar permissões.  
  
    3.  Na área **Explícita** , clique em **Conceder** ou **Negar** ao lado de cada permissão.  
  
7.  Para criar o script do ambiente, clique em **Script**. Por padrão, o script é exibido em uma nova janela do Editor de Consultas.  
  
    > [!TIP]  
    >  Você precisará clicar em **Script** depois de ter feito uma ou mais alterações às propriedades do ambiente, como adicionar uma variável e antes de clicar em **OK** na caixa de diálogo **Propriedades do Ambiente** . Caso contrário, um script não será gerado.  
  
8.  Clique em **OK** para salvar suas alterações nas propriedades de ambiente.  
  
9. No nó **SSISDB** no Pesquisador de Objetos, expanda a pasta **Projetos** , clique com o botão direito do mouse no projeto e, depois, clique em **Configurar**.  
  
10. Na página **Referências** , clique em **Adicionar** para adicionar um ambiente e, depois, em **OK** para salvar a referência para o ambiente.  
  
11. Clique novamente com o botão direito do mouse no projeto e clique em **Configurar**.  
  
12. Para mapear a variável de ambiente para um parâmetro adicionado ao pacote em tempo de criação ou para um parâmetro gerado quando você converteu o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no modelo de implantação de projeto, siga os procedimentos a seguir.  
  
    1.  Na guia **Parâmetros** na página **Parâmetros** , clique no botão Procurar ao lado do campo **Valor** .  
  
    2.  Clique em **Usar variável de ambiente**e selecione a variável de ambiente que você criou.  
  
13. Para mapear a variável de ambiente para uma propriedade de gerenciador de conexões, siga os procedimentos a seguir. Os parâmetros são gerados automaticamente no servidor do SSIS para as propriedades do gerenciador de conexões.  
  
    1.  Na guia **Gerenciadores de Conexões** na página **Parâmetros** , clique no botão Procurar ao lado do campo **Valor** .  
  
    2.  Clique em **Usar variável de ambiente**e selecione a variável de ambiente que você criou.  
  
14. Clique em **OK** duas vezes para salvar as alterações.  
  
  